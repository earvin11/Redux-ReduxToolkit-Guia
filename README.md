---------------------GUIA DE REDUX, REDUX TOOLKIT--------------------

1. Instalar react-redux y @reduxjs/toolkit con el comando: npm install @reduxjs/toolkit react-redux.

2. Crear y configurar el store para eso se crea un archivo independiente llamado store.js que contenga el siguiente codigo:

	import { configureStore } from '@reduxjs/toolkit'

	export const store = configureStore({
  		reducer: {},
	})

3. Proveer el store a toda la aplicacion, en el punto mas alto de los componentes, utilizando el Provider de react-redux y se le envia el store:

	import React from 'react'
	import ReactDOM from 'react-dom'
	import './index.css'
	import App from './App'
	import { store } from './app/store'
	import { Provider } from 'react-redux'

	ReactDOM.render(
  		<Provider store={store}>
    			<App />
  		</Provider>,
  		document.getElementById('root')
	)

4. Crear un slice de redux-toolkit:

	import { createSlice } from '@reduxjs/toolkit'

	const initialState = {
  		value: 0,
	}

	export const counterSlice = createSlice({
  		name: 'counter',
  		initialState,
  		reducers: {
    			increment: (state) => {
      				state.value += 1
    			},
    			decrement: (state) => {
      				state.value -= 1
    			},
    			incrementByAmount: (state, action) => {
      				state.value += action.payload
    			},
  		},
	})

	// Action creators are generated for each case reducer function
	export const { increment, decrement, incrementByAmount } = counterSlice.actions

5. Agregar el reducer del slice en el store, para esto se la da un nombre seguido del reducer:

	import { configureStore } from '@reduxjs/toolkit'
	import { counterSlice } from '../features/counter/counterSlice'

	export const store = configureStore({
  		reducer: {
    			counter: counterSlice.reducer,
  		},
	})