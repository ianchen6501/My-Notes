### 簡介
2017年推出，node.js 的後端框架，可用 javascript / typescript(官網推薦)

### 基本構成
- Modules
- Controllers
- Providers  
Services  
Pipes  
Guards  
Interceptors  
...

> nest.js 利用 modules 來建構應用，任何nest.js的應用程式一定至少要有一個Root Module，並且會依功能區分建立不同 module，例如v下面的就是透過 `.create` 建立一個 `ApplicationModule`
```js
const app = await NestFactory.create(ApplicationModule);
```


>Module通常是一個Class並宣告@Module Decorator，指定哪些Controller及Provider在這個Module使用，通常通一個Controller及Provider不能指定給多個Module。
```js
//app.module.ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```


### DTO(data transfer object)