# Kodlar

## A

### var const let

```js
var x = 5;
x = "Kayseri"
console.log(x);

let y = "Kayseri";
y = "Manisa"
console.log(y);

const z = "Kayseri";
z = "Manisa";
console.log(z);
```

### if else

```js
const saat = new Date().getHours();
if (saat>20){
    console.log("20'den sonra kapalıyız!");
} else {
    console.log("Hoş Geldiniz!");
}
```

```js
const saat = new Date().getHours();
const dakika = new Date().getMinutes();
if (saat>20 && dakika>30){
    console.log("20.30'dan sonra kapalıyız!");
} else {
    console.log("Hoş Geldiniz!");
}
```

```js
const saat = new Date().getHours();
const dakika = new Date().getMinutes();
if (saat>20 && dakika>30){
    console.log("20.30'dan sonra kapalıyız!");
}
else if (saat<8>) {
    console.log("Saat 8'de açılıyoruz!");
}
else {
    console.log("Hoş geldiniz!");
}
```

### Fonksiyonlar

```js
function selamla(isim){
    console.log("Merhaba " + isim);
}

selamla("Ahmet");
```

```js
function YasHesapla(yil){
  const suAn = new Date();
  const buSene = suAn.getFullYear();
  const yas = buSene - yil;
  if (yas>18){
    console.log("Çocuk")
  }
  else if (yas>=18 && yas<=65){
    console.log("Yetişkin")
  }
  else {
    console.log("Yaşlı")
  }
  return yas;
}

const yasim = YasHesapla(2002);
console.log(yasim);
```

### npm

```bash
npm init -y
npm install currency-converter-lt
```

```js
const CC = require('currency-converter-lt')
const currencyConverter = new CC({from: "USD", to: "TRY", amount:1})

currencyConverter.convert().then(response => {
  console.log(`1 Dolar: ${response}TL`)
})
```

## Met

### modül yükleme

```bash
npm init -y
npm i dotenv discord.js@13
```

discord.com/developers

### dotenv .env

```bash
TOKEN=SitedenKopyaladığınızToken
```

### Ana dosya index.js

```js
const Discord = require('discord.js') // Discord.js kütüphanesini dahil edin

const client = new Discord.Client() // Discord.Client sınıfından bir nesne oluşturun

require('dotenv').config() // .env dosyasını dahil edin


client.on('ready', () => { // Bot hazır olduğunda
    console.log('Bot hazır!'); // Konsola "Bot hazır!" yaz
})

client.on('message', message => { // Bir mesaj geldiğinde

    if (!message.author.bot) return // bot mesajlarını iptal et

    if (message.content == 'Merhaba') { // Mesaj "!merhaba" ise
      message.reply('Merhaba!'); // Mesaja Merhaba! diye cevap ver
    }

})

client.login(process.env.TOKEN); // Giriş işlemi
```

### Hoş geldin güle güle

```js
client.on('guildMemberAdd', member => { // Bir üye sunucuya katıldığında
    member.send('Hoş geldin!'); // Üyeye Hoş geldin! mesajı gönder
    member.guild.channels.cache.get('KANAL_ID').send('Hoş geldin ' + member.mention) // Üyeyi sunucuya hoş geldin mesajıyla karşılaştır
})
client.on('guildMemberRemove', member => { // Bir üye sunucudan ayrıldığında
    member.send('Güle güle!'); // Üyeye Güle güle! mesajı gönder
    member.guild.channels.cache.get('KANAL_ID').send('Güle güle ' + member.tag) // Üyeyi sunucudan güle güle mesajıyla karşılaştır
})
```

### Zar Atma Komutu

```js
client.on('message', message => { // Bir mesaj geldiğinde

    if (!message.author.bot) return // bot mesajlarını iptal et

    if (message.content == '!zar') { 
      const sayı = Math.floor(Math.random() * 6)
      message.reply(`Zar **${sayı}** geldi.`);
    }
})
```

### Avesis

```bash
npm i avesis-api
```

```js
const avesisapi = require('avesis-api'); // AvesisAPI kütüphanesini dahil edin

client.on('message', async message => { // Bir mesaj geldiğinde

    if (!message.author.bot) return // bot mesajlarını iptal et

    if (message.content == '!zar') { 
        const sayı = Math.floor(Math.random() * 6)
        message.reply(`Zar **${sayı}** geldi.`); 
    }
    if (message.content.startsWith('!avesis')) {
        const teacherName = message.content.slice(7)
        if (!teacherName) return message.reply('Avesis komutu kullanımı: !avesis <öğretmen id>')

        const docs = await avesisapi.getDocuments({
            university: "kayseri", // required, University name in URL
            teacher: teacherName, // required, Teacher name in URL required
            limit: 5,
        })

        const list = docs.list.map((doc, index) => `**${doc.title}**\n${doc.description}\n\n`).join('\n')

        const embed = new Discord.MessageEmbed()
            .setTitle(`Avesis - ${docs.teacher.name}`)
            .setColor('RANDOM')
            .setDescription(list)
    
        message.reply({ embeds: [embed] })
    }
})
```
