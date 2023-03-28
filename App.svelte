<script>

import { afterUpdate } from 'svelte';

import {
  App,
  Page,
  Navbar,
  List,
  ListItem,
  Checkbox,
  Block,
  BlockTitle,
  Button,
  Toggle,
  NavbarBackLink,
  Link
} from 'konsta/src/svelte';

let theme = 'ios';
let darkMode = false;
let rtl = false;
let isPreview = false;
const toggleRtl = () => {
  rtl = !rtl;
  if(rtl){
    document.dir = 'rtl';
  }else{
    document.dir = 'ltr';
  }
};
const toggleDarkMode = () => {
  darkMode = !darkMode;
  document.documentElement.classList.toggle('dark');
};
afterUpdate(() => {
  darkMode = document.documentElement.classList.contains('dark');
});

</script>
<App theme={theme}>
  <Page>
    <Navbar
      title="My App"
      subtitle="Subtitle"
    >
      <svelte:fragment slot="left">
        {#if !isPreview}
          <NavbarBackLink onClick={() => history.back()} />
        {:else}
          <Link navbar>Left</Link>
        {/if}
      </svelte:fragment>
      <Link slot="right" navbar>Right</Link>
    </Navbar>

    <BlockTitle>Test</BlockTitle>

    <List strongIos outlineIos>
      <ListItem title="RTL" label>
        <Toggle
          slot="after"
          component="div"
          onChange={() => toggleRtl()}
          checked={rtl}
        />
      </ListItem>
      <ListItem title="Preview Mode" label>
        <Toggle
          slot="after"
          component="div"
          onChange={() => isPreview=!isPreview}
          checked={isPreview}
        />
      </ListItem>
    </List>

    <List strongIos outlineIos>
      <ListItem title="Dark Mode" label>
        <Toggle
          slot="after"
          component="div"
          onChange={() => toggleDarkMode()}
          checked={darkMode}
        />
      </ListItem>
    </List>
    <BlockTitle>Theme</BlockTitle>
    <List strongIos outlineIos>
      <ListItem
        label
        title="iOS Theme"
      >
        <Checkbox
          slot="media"
          checked={theme === 'ios'}
          onChange={() => theme = 'ios'}
        />
      </ListItem>
      <ListItem
        label
        title="Material Theme"
      >
        <Checkbox
          slot="media"
          checked={theme === 'material'}
          onChange={() => theme = 'material'}
        />
      </ListItem>
    </List>
    <Block strongIos outlineIos>
      <p>Hello, this is my awesome App</p>
    </Block>
    <Block strongIos outlineIos class="flex space-x-4 rtl:space-x-reverse">
      <Button>Button 1</Button>
      <Button>Button 2</Button>
    </Block>
  </Page>
</App>