# Projeto 1: Curriculum App

Neste projeto, você construirá um aplicativo para exibir seu currículo, explorando alguns recursos de estilos e componentes com o React Native. Acompanhe o tutorial com atenção para reproduzir as configurações iniciais da nossa aplicação. Atenção: é importante não copiar o código inteiro para fixar melhor o aprendizado!

## Estrutura da aplicação

Nossa aplicação estará hospedada na plataforma [expo](https://expo.dev/), com a seguinte estrutura: na pasta `/assets` você poderá colocar as imagens que poderá exibir na aplicação; na pasta `/components` você poderá criar os componentes individuais, sempre com o padrão do nome do componente como subpasta, conforme o exemplo abaixo, e dentro desta subpasta, os arquivos `index.js` e `styles.js`; por fim, no diretório raiz, o arquivo de ponto de partida da aplicação, `App.js`, o arquivo de estilos `styles.js` e o arquivo de dependências `package.json`.

Logo, a estrutura da nossa aplicação será da seguinte forma:

```
/assets
    - icon.png
/components
    /ComponentExample
        - index.js
        - styles.js
- style.js
- App.js
- package.json
```

Antes de começar, abra o arquivo `package.json` e configure as seguintes dependências:
```
{
  "dependencies": {
    "react-native-paper": "3.6.0",
    "react-native-vector-icons": "*",
    "react-native-vector-icons/Feather": "*"
  }
}
```

Nosso aplicativo terá o seguinte design: uma foto, o nome, a função desejada, os links das redes sociais e as informações dispostas em uma lista de cartões.

Antes, vamos preparar a estrutura básica no arquivo que é o ponto de partida, `App.js`:

```
import * as React from 'react';
import { Text, View, StyleSheet } from 'react-native';
import styles from './styles';

const App = () => {
  return (
    <SafeAreaView style={styles.page}>
        // você irá adicionar seus componentes aqui
    </SafeAreaView>
  );
}

export default App;
```

Lembre-se também de adicionar no seu arquivo de estilos `styles.js`, um objeto com um atributo chamado `page`:

```
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  page: {
    flex: 1,
    backgroundColor: '#ecf0f1',
    alignItems: 'center'
  }
});

export default styles;
```

Nesse arquivo nós estamos definindo o Flex Layout, que é um padrão do React Native para dispor os elementos na tela, de forma centralizada, com uma cor de background um pouco cinzenta.

## Configurando a foto e nome do usuário

Para configurar a exibição da foto do usuário, nós vamos criar o primeiro componente contendo a imagem e o texto com o nome do usuário, e ainda a sua função desejada.

Se você configurou uma pasta como no exemplo, `/ComponentExample`, renomeie para `/Avatar` e insira o seguinte código nos arquivos abaixo:

`/components/Avatar/styles.js`
```
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  avatar: {
    width: 150,
    height: 150,
    borderRadius: 125,
    marginTop: 20
  },
  header: {
    alignItems: 'center',
    justifyContent: 'center',
  },
  name: {
    fontSize: 26,
    fontWeight: 'bold',
    marginTop: 10,
  },
  role: {
    marginBottom: 10,
  }
});

export default styles;
```

`/components/Avatar/index.js`
```
import * as React from 'react';
import { Text, View, Image } from 'react-native';
import styles from './styles'

const Avatar = ({name, photo, role}) => (
  <View style={styles.header}>
    <Image source={photo} style={styles.avatar} />
    <Text style={styles.name}>{name}</Text>
    <Text style={styles.role}>{role}</Text>
  </View>
);

export default Avatar;
```

Veja que no primeiro arquivo configuramos os estilos para cada integrante do componente. A foto terá um formato arredondado, por conta da propriedade `borderRadius`. Colocamos algumas margens para deixar a exibição dos nomes mais legível.

No segundo arquivo, observe que qualquer componente que montarmos estará dentro de uma `View`, que será o `parent` dos outros componentes, que o React chama de `children`. 

A função `Avatar` que criamos recebe alguns valores, que estamos usando na forma de **desctructing assigment**. Os valores `name` e `role` que usamos em cada `Text`, fazem parte de um objeto chamado `props`, que são valores passados de um componente para outro.

Para que o seu componente apareça na tela, você deve importar no arquivo ponto de partida. Veja que podemos adicionar as duas props `name` e `role`, as quais falamos anteriormente. Bem elegante, não?

`/App.js`
```
import * as React from 'react';
import { SafeAreaView } from 'react-native';
import styles from './styles';
import photo from './assets/icon.png';
import Avatar from './components/Avatar';

const App = () => {
  return (
    <SafeAreaView style={styles.page}>
      <Avatar photo={photo} name="JOÃOZINHO DOS SANTOS" role="Mobile Developer"/>
    </SafeAreaView>
  );
}

export default App;
```

## Configurando as redes sociais

Vamos criar um novo componente, uma lista das redes sociais do usuário. Cada opção será um botão, usando o componente `TouchableOpacity`, que abre um `Alert` com o link da respectiva rede social, e estará disposto como um ícone da biblioteca de ícones que adicionamos.

Vamos começar com um ícone, do github:

`/components/SocialNetworks/index.js`
```
import * as React from 'react';
import { View, Alert, TouchableOpacity } from 'react-native';
import Icon from 'react-native-vector-icons/Feather';
import styles from './styles';

const SocialNetworks = () => {  
  return (
    <View style={styles.networks}>
      <TouchableOpacity>
        <Icon name="github" size={30} />
      </TouchableOpacity>
    </View>
  )
}

export default SocialNetworks;
```

Vamos adicionar os estilos do nosso componente:

`/components/SocialNetworks/styles.js`
```
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  networks: {
    alignItems: 'center',
    justifyContent: 'space-around',
    width: '80%',
    flexDirection: 'row'
  }
});

export default styles;
```

Como estamos configurando um botão, se faz necessário adicionar uma função para capturar o clique do botão e abrir o alerta com o link correspondente. Então, adicionando os outros ícones, faremos uso da função:

`/components/SocialNetworks/index.js`
```
import * as React from 'react';
import { View, Alert, TouchableOpacity } from 'react-native';
import Icon from 'react-native-vector-icons/Feather';
import styles from './styles';

const SocialNetworks = () => {  
  const handleSocialNetwork = network => {
    switch (network) {
      case 'linkedin':
        Alert.alert('Meu Linkedin', 'https://linkedin.com')
        break
      case 'github':
        Alert.alert('Meu Github', 'https://github.com')
        break
      case 'facebook':
        Alert.alert('Meu Facebook', 'https://facebook.com')
        break
  }

  return (
    <View style={styles.networks}>
      <TouchableOpacity onPress={() => handleSocialNetwork('github')}>
        <Icon name="github" size={30} />
      </TouchableOpacity>
      <TouchableOpacity onPress={() => handleSocialNetwork('facebook')}>
        <Icon name="facebook" size={30} />
      </TouchableOpacity>
      <TouchableOpacity onPress={() => handleSocialNetwork('linkedin')}>
        <Icon name="linkedin" size={30} />
      </TouchableOpacity>
    </View>
  )
}

export default SocialNetworks;
```

Para que esse novo componente seja exibido na tela principal, basta adicionar no arquivo de ponto de partida:

`App.js`
```
import * as React from 'react';
import { SafeAreaView } from 'react-native';
import styles from './styles';
import photo from './assets/icon.png';
import Avatar from './components/Avatar';
import SocialNetworks from './components/SocialNetworks'

const App = () => {
  return (
    <SafeAreaView style={styles.page}>
      <Avatar photo={photo} name="JOÃOZINHO DOS SANTOS" role="Mobile Developer"/>
      <SocialNetworks />
    </SafeAreaView>
  );
}

export default App;
```
## Configurando as Informações

Por fim, insira mais uma pasta em `/components` chamada `/CardItem` e vamos criar nosso componente do cartão que terá as informações como objetivos, experiência profissional e formação acadêmica.

Vamos variar um pouco, e fazer o uso do `children`, que faz parte das `props` (usado novamente na forma de desctructing assigment), construindo o componente apenas com os elementos `View` e `Card`. 

`/components/CardItem/index.js`
```
import React from 'react';
import { View, Text } from 'react-native';
import { Card } from 'react-native-paper';
import styles from './styles';

const CardItem = ({title, children}) => (
  <Card styles={styles.card}>
    <View>
      <Text styles={styles.title}>{title}</Text>
    </View>
    <View style={styles.content}>
      {children}
    </View>
  </Card>
);

export default CardItem;
```

Não se esqueça de configurar os estilos desse componente:

`/components/CardItem/styles.js`
```
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  card: {
    width: '80%',
    justifyContent: 'center',
    marginTop: 15,
    padding: 10
  },
  title: {
    fontWeight: 'bold',
    marginBottom: 10
  },
  content: {
    marginBottom: 10
  }
});

export default styles;
```

Para que esse novo componente seja exibido na tela principal, basta adicionar no arquivo de ponto de partida:

`App.js`
```
import * as React from 'react';
import { Text, SafeAreaView } from 'react-native';
import styles from './styles';
import photo from './assets/icon.png';
import Avatar from './components/Avatar';
import SocialNetworks from './components/SocialNetworks'
import CardItem from './components/CardItem/index'

const App = () => {
  return (
    <SafeAreaView style={styles.page}>
      <Avatar photo={photo} name="JOÃOZINHO DOS SANTOS" role="Mobile Developer"/>
      
      <SocialNetworks />
      
      <CardItem title="Objetivo">
        <Text style={{color: '#939393'}}>Primeira Contratação</Text>
      </CardItem>

      <CardItem title="Formação Acadêmica">
        <Text style={{color: '#939393'}}>Graduação em Ciência da Computação</Text>
      </CardItem>

      <CardItem title="Experiência Profissional">
        <Text style={{color: '#939393'}}>Júnior (1 ano)</Text>
      </CardItem>

    </SafeAreaView>
  );
}

export default App;
```

Veja que o estilo do texto, por usar `children`, é definido inline.

Chegamos ao fim desse primeiro projeto. Espero que você tenha aprendido. Refaça algum passo ou modifique alguma coisa se achar necessário. 

O projeto completo está disponível neste [link](https://snack.expo.dev/@ramon_uepb/curriculum_app).