---
title: Formulários com React
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Aprenda a desenvolver formulários solidos com react.
---
# 🚀 Introdução
Boa parte da interação com aplicações web é feita por meio de [[01 - Notes/Code/HTML/Formulário| formulários]], a primeira vista parecem ser de fácil construção e manipulação, principalmente com _React_, porem um formulário bem construído engloba diversas caracterizas e "reatividades".
Para melhor gestão dos mesmo é muito recomendado o uso da _lib React Hook Forms.

![[Desenho_ReactForm_Introdução|600]]

É de extrema importância se atentar aos estados dos _inputs_ e como manipula-lo dentro do nosso formulário e o estado do próprio formulário pensando e mesclando ideias para encontrar a melhor forma de exibir erros para o usuário.

# 🕹️ Controlled e Uncontrolled
Basicamente _inputs_ do tipo _controlled_ são os que a gente fica ouvindo o estado a todo momento é os _uncontrolled_ é quando os ouvimos apenas em determinados momentos, basicamente.
- _controlled_ - Todo tempo sendo controlado, ouvido.
- _uncontrolled_ - Sem controle, só ouvi em momentos específicos.

##  Capturando Dados (Uncontrolled)
Podemos capturar os dados do nosso formulário de diversas formas, sendo uma das mais simples utilizando a _Web API_ `FormData`, onde a partir da mesma é criada pares de chave e valor, podendo ser acessado e manipulado facilmente.

```js
form.onsubmit( e => {
	e.preventDefault();
	const data = new FormData(e.target);
	window.alert(data.get('name'));
});
```

No exemplo acima estamos pegando o dado de nome que esta no nosso formulário e exibindo no _alert_. Para ==renderizações condicionas essa não é uma boa alternativa==.

## Amarrando Inputs (Controlled)
Para desenvolvermos de fato um _input_ _controlled_, é necessário "amarrar" o nosso componente com um estado, assim conseguindo diversos benefícios, como renderizações condicionais, validação em tempo real, entre outros, Para alcançar tal objetivo, é necessário adicionar o valor do estado ao `value` e na mudança do _input_, ou seja,  no `onChange`, alterar o valor do _input_, assim amarrando completamente estado e input.

```tsx
const [username, setUsername] = useState<String>('');

{...}
<input value={username} onChange={e => setUsername(e.target.value)} />
{...}
```

### Input mais poderoso
Podemos desenvolver componentes controlados (_controlled_) mais poderosos criando um estado melhor construído.

```ts
const [username, setUsername] = useState({
	value: '',
	invalid: true,
	touched: false,
})
```

Assim nosso estado armazenará o valor, controlara a validação do estado, e se o mesmo já foi "tocado", ou seja, se o usuário já entrou no campo. Agora para torna-lo utilizável basta liga-lo ao _input_.

```tsx
<input 
	value={username.value} 
	onBlur={ () => setUsername({
		...username,
		touched: true,
	})}
	onChange={e => {
		if (username.target.value === '') {
			setUsername({
				value: e.target.value,
				invalid: true,
				touched: true,
			}) else {
				setUsername({
				value: e.target.value,
				invalid: false,
				touched: true,
			})
			}
		}
	}}
```

1. Caso clicar e clicar fora, é gravado como tocado para exibir erro.
2. Caso vazio mantem como invalido o valor, caso não, altera o valor e assumi como valido, ambos  identificando como tocado também.

# 📚 Utilizando React Hook Form
Existem diversas bibliotecas para controle de formulários dentro do _React_, atualmente a mais famosa é o _React Hook Form_, por ser extremamente leve e não causar re-renders desnecessário.

>[!tip] Tipos
>A biblioteca já vem com as tipagens para TypeScript.

```sh
yarn add react-hook-form
```

Começamos adicionando a biblioteca ao projeto, em seguida importamos o _hook_ `useForm` e o `SubmitHandler` que utilizamos para tipar, o retorno do _hook_ é desestruturado. 

>[!tip] Configurações
>Dentro da chamada do nosso _hook_ podemos passar um objeto de configuração.
>```tsx
>{...}.useForm({
>	mode: 'all',
>	delayError: 300,
>})
>```

```tsx
import { useForm, SubmitHandler } from "react-hook-form";

type Inputs = {
  example: string,
  exampleRequired: string,
};

export default function App() {
  const { register, handleSubmit, watch, formState: { errors } } = useForm<Inputs>();
  const onSubmit: SubmitHandler<Inputs> = data => console.log(data);

  console.log(watch("example")) // watch input value by passing the name of it

  return (
    /* "handleSubmit" will validate your inputs before invoking "onSubmit" */
    <form onSubmit={handleSubmit(onSubmit)}>
      {/* register your input into the hook by invoking the "register" function */}
      <input defaultValue="test" {...register("example")} />
      
      {/* include validation with required or other standard HTML validation rules */}
      <input {...register("exampleRequired", { required: true })} />
      {/* errors will return when field validation fails  */}
      {errors.exampleRequired && <span>This field is required</span>}
      
      <input type="submit" />
    </form>
  );
}
```

É uma biblioteca muito versátil com fácil integração com qualquer biblioteca para construção UI como `material-ui` que possui um exemplo usando o _hook_ `useControler()`.

# 🎭 Mascaras
Mascara para _inputs_ são de extrema importância para melhor entendimento e visualização do usuário sobre o dado requisitado, muito comum em _inputs_ de telefone, CEP, CPF, entre outros.
Podemos construir e utilizar mascaras utilizando nossos conhecimento em [[Regex]] ou utilizar uma biblioteca famosa chamada `react-input-mask`.

## Regex
Basta criar uma função que utiliza o `replace` juntamente com Regex para definir onde deve ocorrer a alteração, depois basta usar tal função no `onChange` do _input_.

>[!attention] React Hook Form
>Quando utilizado junto ao _React Hook Form_ adicionamos o mesmo dentro do `onChange` do `register`

```ts
export const maskCPF = (value: string) => {
  return value
    .replace(/\D/g, '')
    .replace(/(\d{3})(\d)/, '$1.$2')
    .replace(/(\d{3})(\d)/, '$1.$2')
    .replace(/(\d{3})(\d{1,2})/, '$1-$2')
    .replace(/(-\d{2})\d+?$/, '$1');
};
```

## React Input Mask
Basicamente importamos da biblioteca o componente `ReactInputMask` e passamos para propriedade `mask` a formatação do nosso _input_.

```tsx
import ReactInputMask from 'react-input-mask';

{...}
	<ReactInputMaask mask="999.999.999-99" />
{...}
```

### Utilizando com React Hook Form
Por se tratar de um componente externo é necessário a utilização do `Controller` onde linkaremos o atributo _controller_ do mesmo ao _controller_ do formulário que pode ser obtido através do _hook_ `useForm()`, sem seguida no atributo render é executado uma _callback_ onde recebemos o `field` (desestruturando) e o repassamos para o componente, assim amarando perfeitamente com o formulário.

```tsx
const Register = () => {
  const {register, handleSubmit, control, formState: { errors }} = useForm<Data>({
    mode: 'all',
    delayError: 200,
  });
{...}
	<Controller name="cpf" controller={control} defaultValue="" render={({ field }) => {
		return (
			<ReactInputMask mask="999.999.999-99" {...field} />
		)
	}}
{...}
```

#  Arrays Dinâmicas
É de extrema importancia o uso de `keys` consistentes para a nossa interface não quebrar e ocorrer erros como deletar dois registros ao mesmo tempo, temos algumas ideias para os valores da `keys` como usar _libs_ como CUID ou de forma mais simples usar o `Date.now()` que gera um valor em milissegundos que nunca ira se repetir.

>[!tip] Index
>Podemos utiliza-lo para exibir como ordem para o usuário, mas nunca como `key`

## Função de alteração de item especifico
Função que identifica e altera somente o item e o valor do item que foi alterado.

```typescript
function handleInputchange(key: string, event: React.ChangeEvent<HTMLInputElement>) {
	setProduct( prev => {
		const newState = prev.map( item => {
			if (item.key === key) {
				return {
					...prev,
					[event.taget.name]: event.target.value,
				};
			}
			return item;
		});
		return newState;
	})	
}
```

### Utilizando React Hook Form
Utilizando a biblioteca React Hook Form podemos utilizar a API `useFieldArray` para conseguir o mesmo resultado de forma mais performática, não precisando se preocupar com `keys`.
Podemos deixar o React Hook Form cuidar das chaves para gente, porem se quiser gerenciar isso podemos criar dentro do objeto uma chave com o nome ==rever video para lembrar==