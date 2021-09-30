# Aula 2: Uso de Componentes 

## Componentes

Nessa aula, você irá aprender a criar blocos isolados e livres de outras dependências externas, que permitem a divisão da UI em partes independentes e reutilizáveis, assim como no React para Web.

Antes, é necessário compreender duas estruturas principais dos componentes React: Props, os parâmetros de entrada, e o State, os valores dinâmicos.

### Props

Possibilitam que valores arbitrários sejam passados de um componente para outro.

```
const Usuario = props => { 
	return <Text>Olá, {props.name}</Text>;
}

const App = () => { 
	return <Usuario name="Joaozinho" />
}
```

### State

Um componente contém propriedades que possam ser manipuladas. Logo, se faz necessário utilizar uma estrutura de dados configurada dentro do próprio componente, com valores dinâmicos, o State. Ele não é repassado ao componente, porém é configurado dentro dele.

Podem ser de dois tipos:

#### Componentes com estado (stateful): Usam class Component

```
import React, { Component } from 'react';
import { Text, View } from 'react-native';

const App extends Component {
  state = {
	user: 'Joaozinho'
  };
  render() {
  	return (
    <View>
   <Text>Hello {this.state.user}<Text/>
    </View>
  	)
  }
}
export default App;
```

#### Componente funcional e sem estado* (stateless): Usam functions

*Inclusão dos hooks para proporcionar o gerenciamento de estados nos componentes funcionais

```
import React, { useState } from 'react';
import { Text, View } from 'react-native';

const App = () => {
  const [user, setUser] = useState('Joaozinho');

  return (
    <View>
   <Text>Hello {user}<Text/>
    </View>
  );
}

export default App;
```

## Segundo App: Gerador de Números Aleatórios

Com o que você aprendeu do React para Web e com este conteúdo até aqui, podemos reproduzir um novo exemplo de aplicativo, conforme disposto a seguir:

```
import * as React from 'react';
import {Text, SafeAreaView, Stylesheet, TouchableOpacity}  from 'react-native';

const App = () => {
  const name = 'react';
  
  const [number, setNumber] = useState(0);

  const handleNumber = () => {
    const newNumber = Math.floor(Math.random() * 100);
    setNumber(newNumber);
  }
  return (
    <SaveAreaView style={{styles.container}}>
        <Text>Welcome to UEPB, {name}<Text/>
        <Text>Gerador de Números Aleatórios<Text/>
        <Text style={{styles.number}}>{number}<Text/>
        <TouchableOpacity style={styles.button} 
                onPress={handleNumber}>
 	        <Text>Gerar Número</Text>
        </TouchableOpacity>
    </SaveAreaView>
  );
}

export default App;

const styles = StyleSheet.create({
  container: {
flex: 1,
justifyContent: 'center',
alignItems: 'center',
backgroundColor: '#efefef'
  },
  number: {
    fontSize: 40,
    fontWeight: 'bold',
    color: 'blue'
  },
  button: {
marginTop: 10,
paddingHorizontal: 10,
paddingVertical: 25,
borderRadius: 25,
backgroundColor: 'green',
width: '100%',
alignItems: 'center'
  }
});

```

Esse código pode ser visualizado como stateful neste [link](https://snack.expo.dev/@ramon_uepb/randomic-numbers-2), e como stateless nesse outro [link](https://snack.expo.dev/@ramon_uepb/randomic-numbers).

Esse exemplo é de um componente apenas. Seu próximo passo é reproduzir o Projeto 1 e aprender a criar uma estrutura mais complexa.