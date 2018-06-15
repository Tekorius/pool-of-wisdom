# Renaming React Native Project

It sucks that you cannot set Android package name while creating a project 
(in the time of writing, this may be changed in the future).

A nice npm package was created to solve this issue - `react-native-rename`

1. Install `react-native-rename`

		npm install -g react-native-rename
        
2. Make sure you are in the root of your React Native project
3. Do the rename

		react-native-rename YourApp -b com.yourdomain.yourapp
        
    `-b` is the Android package name flag
    
4. Try running the project again

		react-native run-android
        
## Onoz, it no work!

Yeah that may happen. If it says something like "activity cannot be found" 
or something, try this:

Go to `android/settings.gradle` and see what it includes. If it does not have 
`include :app` line, that's probably what's wrong. For me it was renamed to `include :YourApp`

Thanks to 
[this comment](https://github.com/facebook/react-native/issues/14952#issuecomment-316751765) 
for providing the correct solution!

