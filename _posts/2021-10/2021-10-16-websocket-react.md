---
title: "WebSocket feat. React useContext"
date: 2021-10-16 22:32:00 +0900
classes: wide
tags:
    - tech
    - yumi
    - websocket
    - react
    - react native
    - memo
    - web design
---

`YUMI PROJECT`에서 Notification 구현을 위해 Web Socket을 적용하였다.

## Web Socket

HTTP와 달리 웹소켓은 전이중 통신을 사용하며, 웹소켓은 TCP 위에서 메시지 스트리밍을 가능하게하여 실시간으로 서버 - 클라이언트간 메세지를 주고 받거나 할 때 사용한다. 보통 채팅 앱에서 상대방이 메세지를 입력중인 것을 확인 할 수 있는 것도 바로 이 웹소켓 기술로 연결(connect) 되어 있기 때문에 가능하다.

여기서 connection을 계속(continuously) 열어놓고 있는 것이 가장 큰 차이점이라고 할 수 있겠다.

## react Context

react에서 계속 Top-down 형태로 props를 전달하면 굉장히 번거로워질 일이 생긴다. `Context`는 마치 전역 변수 처럼 props로 전달하지 않고도 쓰고자하는 변수나 오브젝트들을 쓸 수 있게 해준다.

[docs](https://reactjs.org/docs/context.html)

## source code

구현 모습

`WebSocket.js`를 아래와 같이 만들어서 전체 앱에 'Provider' 형태로 감쌌다. 이렇게 감싸게 되면 react Context를 이용해서 WebSocket Provider로 감싸진 어떤 곳에서든 불러 올 수 있다.

실제 구현 코드에서 일부만 발췌했다.

```javascript
// WebSocket.js
import React, { createContext } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { getNotificationSuccess } from '@store/actions';
import * as api from '@api';

const WebSocketContext = createContext(null)

export { WebSocketContext }

export default ({ children }) => {
  let socket;
  let ws;
  let message;

  const user = useSelector(state => state.user);
  
  // TODO : Notification dispatch
  const dispatch = useDispatch();

  if(!socket) {
    socket = new WebSocket(`ws://your_uri`)
    
    socket.onopen = () => {
      console.log('web socket opend')
      // do nothing
    };

    socket.onmessage = (e) => {
      console.log('web socket got message');

      const data = JSON.parse(e.data)
      console.log(data)

      switch(data.type) {
        case 'DEV_SYSTEM_MESSAGE':
          console.log('DEV type message');
          break;
        case 'DEV_NOTIFICATION':
          console.log('Dev Notification')
          dispatch(getNotificationSuccess(data.notification));
          break;
        default:
          console.log(e);
          message = 'hi'
      }
    };

    socket.onerror = (e) => {
      console.log('web socket error');
      console.log(e.message);
    };

    socket.onclose = (e) => {
      console.log('web socket closed');
      console.log(e.code, e.reason);
    };

    ws = {
      socket: socket,
      test: 'hi',
      message: message,
      // function
    }
  }

  return (
      <WebSocketContext.Provider value={ws}>
          {children}
      </WebSocketContext.Provider>
  )
}
```

```javascript
// App.js
import WebSocketProvider from '@api/WebSocket';

export default YumiApp = props => {

  return (<Provider store={store}>
      <WebSocketProvider>
          <Router />
      </WebSocketProvider>
  </Provider>);
}
```

```javascript
// component.js
import { WebSocketContext } from '@api/WebSocket';
import React, { useContext } from 'react';

const ws = useContext(WebSocketContext);
console.log(ws.message)
```

## 참고

[Link](https://www.pluralsight.com/guides/using-web-sockets-in-your-reactredux-app)