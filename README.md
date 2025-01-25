# React Native useCallback Hook with useState Dependency Issue

This repository demonstrates a common, yet subtle, bug encountered when using the `useCallback` hook in React Native with functions that depend on values from `useState`.  The problem arises when the state variable changes, but the memoized function doesn't update accordingly, leading to stale closures and unexpected behavior.

## Problem

The `useCallback` hook is designed to prevent unnecessary re-renders by memoizing a function. However, if the function depends on a state variable, simply including the state variable in the dependency array isn't always sufficient. The function might not re-render correctly if something else outside the function, or if it's a complex state update causing a change that `useCallback` doesn't detect. 

The provided `bug.js` file shows this issue. The increment function uses the `count` state variable. Although `count` is added to the dependency array, it still leads to incorrect behavior.

## Solution

The solution involves carefully considering what to include within the `useCallback` dependency array, and use functional updates for state variables. This is demonstrated in `bugSolution.js`, ensuring that the function re-renders when the state actually updates.

## How to reproduce:

1. Clone this repository.
2. Run `npm install`.
3. Run the application on your React Native environment (e.g. Expo Go, Android emulator).
4. Observe the button click behaviour and the inconsistencies.