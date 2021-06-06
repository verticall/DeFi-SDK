# DeFi-SDK

Client-side-focused DeFi SDK.

# Usage

Just run it in localhost then open the console and check `DeFi` variable for commands
เปิดเว็บใน localhost แล้วเปิด console ขึ้นมา จากนั้นลองดูตัวแปร `DeFi` จะพบกับคำสั่งที่ใช้ได้

![image](https://user-images.githubusercontent.com/7013039/120934310-09aec500-c728-11eb-8e29-6a859753bd49.png)

# Example 1: Swap (Buy) token if the price drop below certain value
ตัวอย่างการเฝ้าราคา ถ้าราคาร่วงมาแตะจุดที่ต้องการ ก็จะซื้ออัตโนมัติ
ระวังอย่าใช้ wallet ประจำนะครับ ควรสร้าง wallet ใหม่สำหรับโปรเจคนี้โดยเฉพาะ

```javascript
DeFi.setWallet('Your private key or Mnemonic'); // don't use your active wallet here. create new one for this project instead.

DeFi.provider.on('block', async n => { // listen to new block event

    let price = await DeFi.Twindex.DOP_BUSD.price(); // get DOP price

    console.log('Block', n, 'DOP Price', price, 'BUSD'); // show info

    if(price <= 1.25){ // if DOP price drop below 1.25 BUSD
        
        // stop listening to new block event
        DeFi.provider.off(); 
        
        // swap all BUSD in the wallet to DOP
        console.log(await DeFi.Twindex.swap(amount = await DeFi.Tokens.BUSD.balance(), from = 'BUSD', to = 'DOP')); 
  
    }

});

```

# Example 2: Swap (Sell) token if the price reached certain value
ตัวอย่างการเฝ้าราคา ถ้าราคาขึ้นไปแตะจุดที่ต้องการ ก็จะขายอัตโนมัติ
ระวังอย่าใช้ wallet ประจำนะครับ ควรสร้าง wallet ใหม่สำหรับโปรเจคนี้โดยเฉพาะ

```javascript
DeFi.setWallet('Your private key or Mnemonic'); // don't use your active wallet here. create new one for this project instead.

DeFi.provider.on('block', async n => { // listen to new block event

    let price = await DeFi.Twindex.DOP_BUSD.price(); // get DOP price

    console.log('Block', n, 'DOP Price', price, 'BUSD'); // show info

    if(price >= 5){ // if DOP price reached 5 BUSD
        
        // stop listening to new block event
        DeFi.provider.off(); 
        
        // swap all DOP in the wallet to BUSD
        console.log(await DeFi.Twindex.swap(amount = await DeFi.Tokens.DOP.balance(), from = 'DOP', to = 'BUSD')); 
  
    }

});

```
