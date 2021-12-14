---
title: "TypeScript - Basic"
date: 2021-12-14 22:29:00 +0900
classes: wide
tags:
    - tech
    - yumi
    - typescript
    - memo
    - web design
---

TypeScript 적용하다가 맨땅에 헤딩한 것들.

## tsconfig.json

```json
{
  "compilerOptions": {
    "allowSyntheticDefaultImports": true,
    "composite": true,
    "declaration": true,
    "esModuleInterop": true,
    "incremental": true,
    "jsx": "react",
    "module": "esnext",
    "moduleResolution": "node",
    "noEmitOnError": true,
    "noImplicitAny": true,
    "noUnusedLocals": true,
    "preserveWatchOutput": true,
    "resolveJsonModule": true,
    "outDir": "lib",
    "rootDir": "src",
    "strict": true,
    "strictNullChecks": true,
    "target": "es2017",
    "types": []
  },
  "include": ["src/**/*"]
}
```

이 때, include가 `src/*`로만 되어 있으면, src하위의 폴더에 들어간 index.ts는 인식하지 못한다. src 구조 안에 폴더를 더 만들게 된다면 꼭 유의하자.
