---
title: Context API
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Entenda quando e como usar Context API
---
# 🚀 Introdução
Basicamente o _React_ é baseado em componentes, e é comum a necessidade de passar informações, por exemplo [[Introdução ao React#Estados|estados]], para diversos componentes, criando uma cadeia de passagem através das [[Componentes#Propriedades|propriedades]], porem as vezes essa informação e usada em diferentes pontos e necessitando de uma grande passagem de propriedades, normalmente até 2 mantem em propriedades acima quando necessário é interessante utilizar o contexto, onde todos os componentes dentro desse contexto tem acesso as informações contidas no mesmo, sem a necessidade de haver passagem através de propriedades.

![[Desenho_React_ContextAPI|600center]]

Podemos possuir vários contextos encadeados, onde os filhos de todos por consequência tem acesso a todos os contextos.
Podemos possuir contexto para componentes específicos, por exemplo.

![[Desenho_React_ContextAPI_ComponentesEspecificos|600center]]

Assim quando o contexto atualizar, com componentes ligados a ele serão re-renderizados automaticamente.

# 🏗️ Criando Contexto
Para desenvolver o nosso contexto iniciamos criando um diretório com o nome `context` onde no mesmo armazenaremos os contextos da nossa aplicação, onde por conversão deve ser nomeado da seguinte forma `NomeContext`, por exemplo um contexto de usuário `UserContext`.
Para iniciar o desenvolvimento do contexto é necessário importar `craeteContext` do _react_.

>[!info] DefaultValue
>Na maioria das vezes contextos tem seu valor populado na medida da execução da aplicação, onde por consequência, normalmente possui deu `DefaultValue` sendo `undefined`.
>```ts
>const UserContext = createContext(undefined);
>```

Basicamente dentro do contexto criado teremos acesso a propriedade `Provider`, onde tudo que estiver dentro deste componente terá acesso ao contexto.
Dentro da propriedade `value` passamos os dados do contexto.

```tsx
const user: IUser = { username: 'john' };

<UserContext.Provider value={user}>
	<App />
</UserContext.Provider>
```

Afim de trazer mais poderes para o nosso contexto e isola-lo para facilitar manutenção, normalmente ==isolamos um contexto dentro de um componentes, onde por se tratar de um componentes _React_ comum temos acesso a tudo, como por exemplo estados com _useStates_==

```tsx
const UserContext = createContext = createContext<IUser | undefined>(undefined);

type UserProviderProps => {
	children: React.ReactNode;
}

const [ user, setUser ] = useState<IUser>();

const UserProvider = ({ childre }: UserProviderProps) => {
	return (
		<UserContext.Provider value={user}>
			{children}
		</UserContext.Provider>
	)
}
```

Basicamente podemos concluir que um ==contexto nada mais é do que tornar publico para todos os seus filhos o que desejarmos==, seja estados, funções, entre outros.

# 🪝Consumindo
Podemos consumir nosso contexto através de um [[Hooks|hook]] do _React_, sendo ele o [[Hooks#useContext|useContext]], onde de forma inteligente podemos eliminar a necessidade de importação do contexto onde o mesmo será consumdo, criando um [[Hooks#Hooks Customizados|hook customizado]] dentro do nosso contexto e o exportando. (Pois dentro do nosso contexto já tem o contexto, ou seja, elimina a necessidade de importação do contexto e do `useContext`, onde será usado, basta importar apenas o _hook_)

```tsx
export const useUser = () => {
	const context = useContext(UserContext);
	
	if (!context) {
		throw new Error('useUser must be used within a UserProvider');
	}
	
	return context;
} 
```

Assim abstraindo através de um _hook_, onde basicamente onde iremos consumir nosso contexto, basta chamar o _hook_ que desenvolvemos, tudo isso sendo possível através do isolamento do nosso contexto.