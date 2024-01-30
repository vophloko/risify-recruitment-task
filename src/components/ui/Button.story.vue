<script setup lang="ts">
import { Button } from '@/components/ui'
import { RouterView } from 'vue-router'
import { createRouter, createMemoryHistory } from 'vue-router'
import { logEvent } from 'histoire/client'

function setupApp({ app }: { app: any }) {
  app.use(
    createRouter({
      history: createMemoryHistory(),
      routes: [
        { path: '/', name: 'home', component: { render: () => 'Home' } },
        { path: '/about', name: 'about', component: { render: () => 'About' } }
      ]
    })
  )
}
</script>

<template>
  <Story title="Button" :setup-app="setupApp">
    <Variant title="Sizes">
      <div>
        <Button size="large">Large Button</Button>
        <Button size="regular">Regular Button</Button>
        <Button size="small">Small Button</Button>
      </div>
      <Button block>Block Button</Button>
      <Button
        ><span
          ><template v-for="i in 10" :key="i"
            >Button With Overflowing Content <template v-if="i !== 10"> | </template></template
          ></span
        ></Button
      >
    </Variant>
    <Variant title="Variants">
      <Button variant="filled">Filled Button</Button>
      <Button variant="filled" color="yellow">Yellow Filled Button</Button>
      <Button variant="outlined">Outlined Button</Button>
      <Button variant="outlined" color="yellow">Yellow Outlined Button</Button>
    </Variant>
    <Variant title="With onClick event">
      <Button @click="logEvent('click', $event)"
        >Click me and inspect "Events" tab on your right</Button
      >
    </Variant>
    <Variant title="Disabled">
      <Button>Focusable Button</Button>
      <Button @click="logEvent('click', $event)" disabled>Disabled Button</Button>
      <Button>Focusable Button</Button>
    </Variant>
    <Variant title="With an icon">
      <div>
        <Button>
          <template #prepend>
            <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24">
              <path fill="currentColor" d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6z" />
            </svg>
          </template>

          Button with Prepended Icon
        </Button>
        <Button
          >Button with Appended Icon
          <template #append>
            <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24">
              <path fill="currentColor" d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6z" />
            </svg>
          </template>
        </Button>
      </div>
    </Variant>
    <Variant title="With an image">
      <div>
        <Button>
          <template #prepend>
            <img src="https://images.dog.ceo/breeds/mountain-swiss/n02107574_2383.jpg" alt="Dog" />
          </template>
          Button with Prepended Image
        </Button>
        <Button
          >Button with Appended Image
          <template #append>
            <img src="https://images.dog.ceo/breeds/mountain-swiss/n02107574_2383.jpg" alt="Dog" />
          </template>
        </Button>
      </div>
    </Variant>
    <Variant title="Displayed as <a>">
      <Button as="a" href="https://google.com">Go to Google.com</Button>
    </Variant>
    <Variant title="Displayed as <router-link>">
      <div>
        <Button as="router-link" :to="{ name: 'home' }">Navigate to Home page</Button>
        <Button as="router-link" :to="{ name: 'about' }">Navigate to About page</Button>
      </div>
      <router-view />
    </Variant>
  </Story>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');
</style>
