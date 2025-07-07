// App.js
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import HomeScreen from './screens/HomeScreen';
import ProfileScreen from './screens/ProfileScreen';
import UploadScreen from './screens/UploadScreen';
import { StatusBar } from 'expo-status-bar';
import { auth } from './firebaseConfig';
import { onAuthStateChanged } from 'firebase/auth';
import { useEffect, useState } from 'react';

const Tab = createBottomTabNavigator();

export default function App() {
  const [user, setUser] = useState(null);

  useEffect(() => {
    const unsubscribe = onAuthStateChanged(auth, userAuth => {
      setUser(userAuth);
    });
    return unsubscribe;
  }, []);

  if (!user) {
    return <LoginScreen />;
  }

  return (
    <NavigationContainer>
      <StatusBar style="light" />
      <Tab.Navigator>
        <Tab.Screen name="Home" component={HomeScreen} />
        <Tab.Screen name="Upload" component={UploadScreen} />
        <Tab.Screen name="Profile" component={ProfileScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}// firebaseConfig.js
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";
import { getFirestore } from "firebase/firestore";
import { getStorage } from "firebase/storage";

const firebaseConfig = {
  apiKey: "YOUR_FIREBASE_API",
  authDomain: "YOUR_FIREBASE_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_BUCKET",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};

const app = initializeApp(firebaseConfig);

export const auth = getAuth(app);
export const db = getFirestore(app);
export const storage = getStorage(app);YutTokApp/
│
├── App.js
├── firebaseConfig.js
├── screens/
│   ├── HomeScreen.js
│   ├── ProfileScreen.js
│   ├── UploadScreen.js
│   ├── LoginScreen.js
├── components/
│   ├── VideoPlayer.js
│   ├── VideoCard.js
│   └── Header.js
├── assets/
│   ├── icons/
│   └── logo.png
└── package.json
