# 🎲 Banco de Dados
Foi desenvolvido uma tabela que armazena dos dados dos fornecedores com um ID com auto incremento, nome do fornecedor todo em caixa baixa, sigla para identificação do mesmo e para juntar com o SKU, e a data da inserção.

```sql
CREATE TABLE wp_suppliers(
  id INT UNSIGNED PRIMARY KEY NOT NULL AUTO_INCREMENT,
  name VARCHAR(100)	NOT NULL,
  create_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  prefix VARCHAR(5) NOT NULL
);
```

Em seguida foi criado a coluna para relacionamento na tabela `wp_wc_product_meta_lookup`

```sql
ALTER TABLE wp_wc_product_meta_lookup
        ADD id_supplier INT UNSIGNED;
```

Criando o relacionamento

```sql
   ALTER TABLE wp_wc_product_meta_lookup
ADD CONSTRAINT fk_id_supplier
   FOREIGN KEY (id_supplier)
    REFERENCES wp_suppliers(id);
```

Em seguida foi criado a coluna para armazenar id  do produto do fornecedor, o que vem pela API

```sql
ALTER TABLE wp_wc_product_meta_lookup
				ADD supplier_product_id VARCHAR(20);
```

# 📥 Fluxo do dado
O fluxo dos dados advindo das APIs é, ser identificado os dados através da interface  compatível, passar pela função de `insertOrUpdate` onde é verificado se tal produto já esta adicionado ou não no banco de dados, em seguida o produto é convertido para uma estrutura de dado especifica para ser compatível com a função desenvolvida de _insert_ e _update_

![[Desenho_Lumine_Fluxo.excalidraw|650]]

# 🏗️ Estrutura do Dado
Após a API ser consumida os dados precisam ser convertidos para facilitar o _insert_ e _update_ criando uma função única para os mesmo, todo produto é convertido para seguinte estrutura.

```ts
// Antigo
interface IProduct {
  id: number;
  name: string;
  price: number;
  stock: number;
  description: string;
  shortDescription: string;
  idSupplier: number;
  markup: number;
  variantes?: TVariantes;
}

// Novo
export class Product {
  public readonly variations!: IVariant[];
  public readonly attributes!: TAttribute;
  public dimensions!: IDimensionsWooCommerce;
  public readonly images!: IImage[];
  
  constructor(
    public id: string,
    public name: string,
    public price: number,
    public stock: number,
    public description: string,
    public shortDescription: string,
    public idSupplier: number,
    public markup: number
  ) {
    this.variations = [];
    this.images = [];
    this.attributes = {} as TAttribute;
  }
  
  get finalPrice(): number {
    return this.price + (this.price * this.markup) / 100;
  }
  
  get sku() {
    return `${globalThis.prefixes[this.idSupplier - 1]}${this.id}`;
  }
  
  get slug() {
    return `${globalThis.prefixes[this.idSupplier - 1]}-${this.name
      .toLowerCase()
      .replace(/\s/g, '-')}`;
  }
  
  addAttributeBody(idAttribute: number, attributeName: TAttributeKeys): void {
    this.attributes[attributeName] = {
      id: idAttribute,
      name: attributeName,
      options: [],
    };
  }
  
  addAttributeValue(attributeName: TAttributeKeys, option: string): void {
    this.attributes[attributeName].options.push(option);
  }
  
  updateStockVariation(sku: string, quantity: number): void {
    const variation = this.variations.find((v) => v.sku === sku);
    if (variation) {
      variation.quantity = quantity;
    }
  }
  
  generateVariations(): void {
    const optionsArrays: string[][] = Object.values(this.attributes).map(
     (attribute) => attribute.options

    );
  
    const attributeCombinations: string[][] = this.cartesianProduct(
      ...optionsArrays
    );
  
    attributeCombinations.forEach((attributes) => {
      const sku = `${this.sku}-${attributes.join('-')}`;
      const price = this.finalPrice;
      const stock = this.stock;
      const description = attributes
        .map(
          (attribute, index) =>
            `${Object.keys(this.attributes)[index]}: ${attribute}`
        )
        .join(', ');
  
      this.variations.push({
        sku,
        price,
        finalPrice: price,
        quantity: stock,
        description,
        image: this.images[0], // usa a primeira imagem do produto como padrão
        attributes: Object.fromEntries(
          Object.entries(this.attributes).map(([key, value], index) => 
            key,
            { id: value.id, name: value.name, option: attributes[index] },
          ])
        )
      });
    });
  }

  private cartesianProduct<T>(...arrays: T[][]): T[][] {
    return arrays.reduce<T[][]>(
      (acc, arr) => {
        return acc.flatMap((values) => {
          return arr.map((value) => values.concat(value));
        });
      },
      [[]]
    );
  }
}
```

# 💫 Atributos
Podemos possuir diferentes atributos para os produtos, os mesmos são armazenados em um [[Type#Mapped Types|mapped type]] que como chave tem os nomes dos atributos e como valor recebe uma interface `IVariant` que possui o valor a quantidade em estoque de tal variação e o preço de tal variação.

```ts
type TVariantsName = 'cor';
  
export interface IVariant {
  value: string;
  quantity: number;
  price: number;
  finalPrice: number;
  sku: string;
}
  
type TVariantes = {
  [key in TVariantsName]: IVariant[];
};
```

# 📥 Inserindo e Atualizando Dados
