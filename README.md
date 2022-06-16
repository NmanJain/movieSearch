### Movie Search App

##### Important commands to use in terminal

- `npm install`: installs all dependencies
- `npm run start`: starts the app, then when you see the QR code you can load it directly to your android simulator by pressing "a"

    ###### GitHub commands

    Create a new branch first:
    `git checkout -b my-new-branch-name`
    Make sure you're in the right branch:
    `git switch my-new-branch-name` to switch to it, or `git branch` to see what branch you're on

    Then do your work. Then when you're ready to submit some changes:

    - `git add .`: adds all files to the staging area
    - `git commit -m "message"`: commits the changes to the staging area
    - `git push`: pushes the changes to the remote repository


##### Where important things are located
- [Navigation](navigation/index.tsx): controls the tabs on the bottom of the screen. You can add a new tab by adding a component to the `BottomTabNavigator` section of the `index.tsx`
- [Home](screens/Home/Home.tsx): the main screen for the app that people will see immediately. There is a `components` folder which should contain any components used by the Home screen
- [Search](screens/Search/Search.tsx): the search screen where users can search for movies. There is a `components` folder which should contain any components used by the Search screen
- [components](components): A folder to contain any components that are shared by multiple screens

You should go through this tutorial that will help demonstrate some of the fundamentals: https://reactnative.dev/docs/tutorial

When the tutorial talks about `State`, this is a more advanced topic that defines how things can change and update live. We'll get more into this later, you can play around with it if you'd like to try.

##### How to make a component
1. Create a file in the appropriate components folder called `ComponentName.tsx`
2. Add the following starter code to the file:

```typescript
export const ComponentName = () => {
    return (
        <View>
        {/* your code here */}
        </View>
    )
}
```

3. If the file takes in parameters, create an `interface` that defines the rules, and add the `prop` object to the component

```typescript
interface PropsDefinition {
    someParameter: string;
    anotherParameter: number;
}
export const ComponentName = (props: PropsDefinition) => {
    // Access `someParameter` like this:
    const { someParameter, anotherParameter } = props;
    return (
        <View>
            {/* Use it like this */}
            <Text>My parameter: {someParameter}</Text>
        </View>
    )
}
```

4. Then import the component into the appropriate screen file:

```typescript
import { ComponentName } from './components/ComponentName';

export const HomeScreen = () => {
  return (
    <View>
        <ComponentName someParameter="Hello" anotherParameter={42}/>
    </View>
  );
}
```

##### How to style a component

You'll need to read up on how styling works. There are several core concepts that you'll need to understand:

1. Basic styling: https://reactnative.dev/docs/style
2. Height & width: https://reactnative.dev/docs/height-and-width
3. Layout & Flexbox: https://reactnative.dev/docs/flexbox
4. Images: https://reactnative.dev/docs/images
5. Colors: https://reactnative.dev/docs/colors for this, it's simply referencing color codes and saying `color: 'red'` or `color: '#ff0000'` or `backgroundColor: '#ff0000'` or something similar.

Each screen already has a stylesheet ready to go as an example, you just have to create new StylesSheets and then reference them in components.

```typescript
<Text style={styles.title}>Home</Text>
```
This is referencing the style from the StyleSheet defined in the same file:
```typescript
const styles = StyleSheet.create({
  title: {
    fontSize: 20,
    fontWeight: 'bold',
  },
});
```

##### How to make a button
Buttons are very easy to make. You can use the `TouchableOpacity` component to make a button.

```typescript
import { StyleSheet, Text, View, TouchableOpacity } from 'react-native';

export const HomeScreen = () => {
  return (
    <View style={styles.container}>
      <TouchableOpacity onPress={() => {
        // You can put any logic in here
        console.log("Button pressed!");
      }}>
        <Text>Press me!</Text>
      </TouchableOpacity>
    </View>
  );
}
```

Something more interesting would be to have a button that navigates to a new screen (this gets into state usage. We use the "useNavigation" hook to access our navigation stack). The name we use must correspond to the name of the screen we want to navigate to, which is defined in the `navigation` folder.

```typescript
import { StyleSheet, Text, View, TouchableOpacity } from 'react-native';
import { useNavigation } from '@react-navigation/native';
import { NativeStackNavigationProp } from '@react-navigation/native-stack';

export const HomeScreen = () => {
const navigation = useNavigation<NativeStackNavigationProp<any, any>>();

  return (
    <View style={styles.container}>
      <TouchableOpacity onPress={() => {
          navigation.navigate('Search');
      }}>
        <Text>Press me!</Text>
      </TouchableOpacity>
    </View>
  );
}

```

##### How to make a scrollable list

ScrollView: https://reactnative.dev/docs/scrollview
FlatList: https://reactnative.dev/docs/flatlist (more advanced, but far more powerful)

##### How to add photos

Image: https://reactnative.dev/docs/image