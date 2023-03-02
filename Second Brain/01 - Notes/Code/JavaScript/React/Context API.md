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

## Adicionando Funções
É muito comum disponibilizarmos através de contexto funções que possam executar tarefas especificas, como por exemplo alterar um valor de um estado. Uma pratica muito interessante é criar uma função que recebe como parâmetro o valor e jogo o mesmo para o estado, assim podendo implementar no corpo da função, regras de negócio.

```tsx
interface IUserContext {
	name: string;
	updateUsername(name: string): void;
}

const UserContext = createContext<IUserContext | undefined>(undefined);

export const App = () => {
	const [ user, setUser ] = useState();
	
	function updateUserName(name: string) {
		if (name === `João`) {
			setUser('Proibido!');
			return;
		}
		setUser({
			name: name;
		});
	}
	
	return (
		<UserContext.Provider value={ {...user, updateUsername} }>
			 <App />
		</UserContext.Provider>	
	)
}
```

Assim nosso contexto contem todas as propriedades de `user` que é um estado **(e que possui a estrutura igual uma parte da estrutura da interface do contexto)**, e possui a função que utilizamos para atualizar o valor do `user` que passa por uma "Validação".

>[!attention] Porque apenas o nome da função
>Podemos perceber que foi passado um objeto na propriedade `value` contendo a desestruturação no estado `user` que cobre metade da estrutura da interface do contexto, e a [[Funções#Referencia de Função|referencia de uma função]], podemos notar **que não foi necessário** passar o nome da propriedade que conterá a função, pois, ambas possuem o mesmo nome, assim possibilitando a omissão do mesmo.
>```tsx
>{ ... }
><UserContext.Provider value={ { ...user, updateUsername: updateUsername } }>
>{ ... }
>```
>Caso possuisem nomes diferentes séria necessário informar
>```tsx
>{ ... }
><UserContext.Provider value={ { ..user, updateUsername : teste } }>
>{ ... }
>```

# 📨 Consumindo
Podemos consumir nosso contexto através de um [[Hooks|hook]] do _React_, sendo ele o [[Hooks#useContext|useContext]], onde de forma inteligente podemos eliminar a necessidade de importação do contexto em todo componente onde o mesmo será consumido, criando um [[Hooks#Hooks Customizados|hook customizado]] dentro do nosso contexto e o exportando. (Pois dentro do nosso contexto já tem o contexto, ou seja, elimina a necessidade de importação do contexto e do `useContext`, onde será usado, basta importar apenas o _hook_)

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

# 🪝Adicionando Reducer
O [[Hooks|hook]] [[Hooks#🪝useReducer|useReducer]] e amplamente utilizado em conjunto com contexto, pois, prove um fluxo de atualização de estados muito mais dinâmico facilitando a implementação de estados mais complexos, eliminando a necessidade de criar diversas funções para o mesmo, trazendo mais performance por consequência. Basicamente desenvolveremos um [[Hooks#Reducer|reducer]] que possuirá toda logica para atualização dinâmica, onde nosso contexto possuirá o estado do contexto e um _dispatch_ para atualização do mesmo.
Basicamente nosso contexto possuirá um estado e uma função _dispatch_, onde os mesmo serão preenchidos no `value` do _Provider_, através do resultado do uso do _hook_ _useReducer_.

```tsx
import { userReducer, initialState, ReducerState, ReducerAction } from './context';

interface IUserContext {
  state: ReducerState;
  dispatch(action: ReducerAction): void;
}

type UserContextProps = {
  children: React.ReactNode;
};
  
const UserContext = createContext<IUserContext | undefined>(undefined);
  
export const UserProvider = ({ children }: UserContextProps) => {
  const [state, dispatch] = useReducer(userReducer, initialState);
  return (
    <UserContext.Provider value={ { state, dispatch } }>
      {children}
    </UserContext.Provider>
  );
};
```

>[!tip] Estado Inicial
>Uma  ideia muito utilizada é criar dentro do próprio arquivo que contendo o código do _[[Hooks#Reducer|reducer]]_ um  _initialState_, ou seja, um estado inicial, para passarmos quando utilizarmos o _[[Hooks|hook]]_ _[[Hooks#🪝useReducer|userReducer]]_.
>```ts
>export const initialState: ReducerState = {
>	name: '',
>	id: '',
>	counter: 0,
>}
>```