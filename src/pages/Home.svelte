<script>
  import {
    Page,
    Navbar,
    BlockTitle,
    List,
    ListItem,
    Radio,
    Toggle,
    Link,
    Popover,
  } from 'konsta/svelte';

  import { afterUpdate } from 'svelte';
  import routes from '../routes.js';
  import DemoIcon from '../components/DemoIcon.svelte';

  export let theme;
  export let setTheme;
  export let setColorTheme;
  export let colorPickerOpened;

  let darkMode = false;

  const toggleDarkMode = () => {
    darkMode = !darkMode;
    if(darkMode){
      document.documentElement.classList.add('dark');
    } else {
      document.documentElement.classList.remove('dark');
    }
  };

  let rtl = false;
  const toggleRtl = () => {
    rtl = !rtl;
    if(rtl){
      document.dir = 'rtl';
    }else{
      document.dir = 'ltr';
    }
  };

  afterUpdate(() => {
    darkMode = document.documentElement.classList.contains('dark');
    rtl = document.dir === 'rtl';
  });
</script>

<Page>
  <Navbar title="Konsta UI" large transparent centerTitle />

  <BlockTitle>Theme</BlockTitle>
  <List strong inset>
    <ListItem label title="iOS Theme">
      <Radio
        slot="media"
        onChange={() => setTheme('ios')}
        component="div"
        checked={theme === 'ios'}
      />
    </ListItem>
    <ListItem label title="Material Theme">
      <Radio
        slot="media"
        onChange={() => setTheme('material')}
        component="div"
        checked={theme === 'material'}
      />
    </ListItem>
  </List>
  <List strong inset>
    <ListItem title="RTL" label>
      <Toggle
        slot="after"
        component="div"
        onChange={() => toggleRtl()}
        checked={rtl}
      />
    </ListItem>
    <ListItem title="Dark Mode" label>
      <Toggle
        slot="after"
        component="div"
        onChange={() => toggleDarkMode()}
        checked={darkMode}
      />
    </ListItem>

    <ListItem
      title="Color Theme"
      link
      onClick={() => (colorPickerOpened = true)}
    >
      <div
        slot="after"
        class="w-6 h-6 rounded-full bg-primary home-color-picker"
      />
    </ListItem>
  </List>
  <Popover
    opened={colorPickerOpened}
    onBackdropClick={() => (colorPickerOpened = false)}
    size="w-36"
    target=".home-color-picker"
  >
    <div class="grid grid-cols-3 py-2">
      <Link
        touchRipple
        class="overflow-hidden h-12"
        onClick={() => setColorTheme('')}
      >
        <span class="bg-brand-primary w-6 h-6 rounded-full" />
      </Link>
      <Link
        touchRipple
        class="overflow-hidden h-12"
        onClick={() => setColorTheme('k-color-brand-red')}
      >
        <span class="bg-brand-red w-6 h-6 rounded-full" />
      </Link>
      <Link
        touchRipple
        class="overflow-hidden h-12"
        onClick={() => setColorTheme('k-color-brand-green')}
      >
        <span class="bg-brand-green w-6 h-6 rounded-full" />
      </Link>
      <Link
        touchRipple
        class="overflow-hidden h-12"
        onClick={() => setColorTheme('k-color-brand-yellow')}
      >
        <span class="bg-brand-yellow w-6 h-6 rounded-full" />
      </Link>
      <Link
        touchRipple
        class="overflow-hidden h-12"
        onClick={() => setColorTheme('k-color-brand-purple')}
      >
        <span class="bg-brand-purple w-6 h-6 rounded-full" />
      </Link>
    </div>
  </Popover>

  <BlockTitle>Components</BlockTitle>
  <List strong inset>
    {#each routes as route}
      <ListItem link href={`#${route.path}`} title={route.title}>
        <DemoIcon slot="media" />
      </ListItem>
    {/each}
  </List>
</Page>
