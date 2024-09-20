---
title: 介绍
order: 1
sidemenu: false
---

# 业务组件

前言：为什么写业务组件，想把增删改查中经常用到的比如人员选择器，车辆选择器拿出来，包含接口封装好

## 安装

使用`npm` 或者 `yarn` 安装 `@vortex-ui/biz`的依赖。

```
npm i @vortex-ui/biz -S
```

```
yarn add  @vortex-ui/biz -S
```

```tsx
import React from 'react';
import { Button } from 'antd';
import { CommonApi } from 'vtx-snd-api';

export default class Index extends React.Component {
  async login(item) {
    const res = await CommonApi.management.login({
      password: item.password,
      username: item.username,
    });
    if (res.data && res.result === 0) {
      console.log(res);
      saveLocalStorage({
        tenantId: res.data.tenantId,
        userId: res.data.userId,
        access_token: '657cae70-6d7a-481b-a15a-cbced5d66990',
      });
    }
  }

  render() {
    const accounts = [
      {
        name: '张全蛋',
        password: '2bda371afe3c1e257ca02d218f76c6b7',
        username: 'testV2',
      },
    ];
    return (
      <>
        {accounts.map((item) => (
          <Button onClick={() => this.login(item)} key={item.username}>
            登录{item.name}
          </Button>
        ))}
      </>
    );
  }
}
function saveLocalStorage(DYNAMIC) {
  // 发请求自动登录
  if (DYNAMIC.tenantId && DYNAMIC.userId && DYNAMIC.access_token) {
    try {
      localStorage.setItem(
        'ACCESS-TOKEN',
        JSON.stringify({
          tenantId: DYNAMIC.tenantId,
          userId: DYNAMIC.userId,
          access_token: DYNAMIC.access_token,
          token: DYNAMIC.access_token,
        }),
      );
    } catch (error) {
      console.log('无痕模式，无法存储');
    }
  }
}
```
