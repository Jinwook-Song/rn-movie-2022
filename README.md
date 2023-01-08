# React native

| 프로젝트 기간 | 23.01.07 ~             |
| ------------- | ---------------------- |
| 프로젝트 목적 | Learn eact native      |
| Github        |                        |
| Docs          | https://docs.expo.dev/ |

---

Template

[ignite](https://github.com/infinitered/ignite) vs create react native app([crna](https://github.com/expo/create-react-native-app))

```bash
# Get walked through the prompts for the different options to start your new app
npx ignite-cli@latest new PizzaApp

# Accept all the recommended defaults and get straight to coding!
npx ignite-cli@latest new PizzaApp --yes

-------

npx create-react-native-app
```

- ignite는 자주사용 되는 패키지를 모두 설치하고, 기본적인 폴더 구조가 세팅되어있다
- crna는 native에 접근 가능하면서도 expo sdk를 활용할 수 있도록 해준다

---

### splash screen

`npx expo install expo-splash-screen`

```jsx
import * as SplashScreen from 'expo-splash-screen';
import { useCallback, useEffect, useState } from 'react';
import { Text, View } from 'react-native';

export default function App() {
  SplashScreen.preventAutoHideAsync();

  const [isReady, setIsReady] = useState(false);

  async function wait() {
    await new Promise((resolve) => setTimeout(resolve, 5000));
    setIsReady(true);
  }

  useEffect(() => {
    wait();
  }, []);

  const onLayoutRootView = useCallback(async () => {
    if (isReady) {
      // This tells the splash screen to hide immediately! If we call this after
      // `setAppIsReady`, then we may see a blank screen while the app is
      // loading its initial state and rendering its first pixels. So instead,
      // we hide the splash screen once we know the root view has already
      // performed layout.
      await SplashScreen.hideAsync();
    }
  }, [isReady]);

  if (!isReady) {
    return null;
  }

  return (
    <View
      style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}
      onLayout={onLayoutRootView}
    >
      <Text>SplashScreen Demo! 👋</Text>
    </View>
  );
}
```
