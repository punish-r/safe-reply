# 🔗 **SAFE-REPLY NODEJS**

## 📑 **EXPLICAÇÃO**
> Nessa documentação, trago para vocês uma função para evitar erros como **Interação falhou**, **Interação desconhecida** e **O aplicativo não respondeu** em sua aplicação do Discord. Como todos sabem, o Discord tem um tempo de **3 segundos** para uma resposta; caso passe **de 3,1 segundos**, a interação é deletada e não é mais possível respondê-la.


### 👁️ **ENTENDA MAIS SOBRE INTERAÇÕES**
- Discord [Interacões](https://discord.com/developers/docs/interactions/receiving-and-responding#interactions) 
- Rincko [Explicação de Interações](https://youtu.be/2GbuXzTiR6Q?si=ugk8ztAHBHmNrOK_)

### 📁 **FUNÇÃO**
```js
export async function reply(interaction, options = {}, type = 'reply') {
  try {
    if (type === 'modal') {
      return await interaction.showModal(options);
    }
    
    if (interaction.deferred) {
      return await interaction.editReply(options);
    } else if (interaction.replied) {
      return await interaction.followUp(options);
    } else if (type === 'reply') {
      return await interaction.reply(options);
    } else if (type === 'defer') {
      return await interaction.deferReply(options);
    }
  } catch(err) {
    console.error(`[ replyJS erro ]: `, err.message);
  }
};
```

### 🪛 **COMO USAR**
- Apenas com embed
```js
await reply(interaction, { embeds: [embed] });
```
- Com componentes
```js
await reply(interaction, { embeds: [embed], components: [row] });
```
- Para modal
```js
await reply(interaction, modal, 'modal');
```
- Visualização apenas para você
```js
await reply(interaction, { embeds: [embed], flags: 64 });
```

### 📃 **COMO EXPORTAR**
- ES MODULES
```js
import { reply } from 'pasta/do/arquivo/safe-reply';
```
- COMMON JS
```js
const { reply } = require('./pasta/do/arquivo/safe-reply');
```
