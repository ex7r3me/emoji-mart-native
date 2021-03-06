<div align="center">
  <br><b>Emoji Mart Native</b> is a Slack-like customizable<br>emoji picker component for React Native ported from <a href="https://github.com/missive/emoji-mart/">[Emoji Mart]</a>
  <br><a href="https://thinkproductivity.github.io/emoji-mart-native">Demo</a> #TODO: Make example RN app • <a href="https://github.com/thinkproductivity/emoji-mart-native/releases">Changelog</a>
  <br><br><img width="338" alt="picker" src="https://user-images.githubusercontent.com/12134822/40007137-ecf6cfc2-5793-11e8-9943-08a9ba8c7fee.png">
</div>

## Installation

`npm install --save emoji-mart-native`

## Components
### Picker
Renders *inline-block* & center aligned if parent is wider than picker.
To render picker in a fullscreen modal use [`<ModalPicker />`](#modalpicker).

```jsx
import { Picker } from 'emoji-mart-native'

<Picker set='emojione' />
<Picker onSelect={this.addEmoji} />
<Picker title='Pick your emoji…' emoji='point_up' />
<Picker style={{ position: 'absolute', bottom: 20, right: 20 }} />
<Picker i18n={{ search: 'Recherche', categories: { search: 'Résultats de recherche', recent: 'Récents' } }} />
```

| Prop | Required | Default | Description |
| ---- | :------: | ------- | ----------- |
| **autoFocus** | | `false` | Auto focus the search input when mounted |
| **color** | | `#ae65c5` | The top bar anchors select and hover color |
| **emoji** | | `department_store` | The emoji shown when no emojis are hovered, set to an empty string to show nothing |
| **include** | | `[]` | Only load included categories. Accepts [I18n categories keys](#i18n). Order will be respected, except for the `recent` category which will always be the first. |
| **exclude** | | `[]` | Don't load excluded categories. Accepts [I18n categories keys](#i18n). |
| **custom** | | `[]` | [Custom emojis](#custom-emojis) |
| **recent** | | | Pass your own frequently used emojis as array of string IDs |
| **emojiSize** | | `24` | The emoji width and height |
| **onClick** | | | Params: `(emoji, event) => {}`. Not called when emoji is selected with `enter` |
| **onSelect** | | | Params: `(emoji) => {}`  |
| **onSkinChange** | | | Params: `(skin) => {}` |
| **onPressClose** | | | Trigger when user press back button
| **perLine** | | `9` | Number of emojis per line. While there’s no minimum or maximum, this will affect the picker’s width. This will set *Frequently Used* length as well (`perLine * 4`) |
| **i18n** | | [`{…}`](#i18n) | [An object](#i18n) containing localized strings |
| **native** | | `false` | Renders the native unicode emoji |
| **set** | | `apple` | The emoji set: `'apple', 'google', 'twitter', 'emojione', 'messenger', 'facebook'` |
| **sheetSize** | | `64` | The emoji [sheet size](#sheet-sizes): `16, 20, 32, 64` |
| **backgroundImageFn** | | ```((set, sheetSize) => …)``` | A Fn that returns that image sheet to use for emojis. Useful for avoiding a request if you have the sheet locally. |
| **emojisToShowFilter** | | ```((emoji) => true)``` | A Fn to choose whether an emoji should be displayed or not |
| **showPreview** | | `true` | Display preview section |
| **showSkinTones** | | `true` | Display skin tones picker |
| **emojiTooltip** | | `false` | Show emojis short name when hovering (title) |
| **skin** | | | Forces skin color: `1, 2, 3, 4, 5, 6` |
| **defaultSkin** | | `1` | Default skin color: `1, 2, 3, 4, 5, 6` |
| **style** | | | Inline styles applied to the root element. Useful for positioning |
| **title** | | `Emoji Mart™ Native` | The title shown when no emojis are hovered |
| **showBackButton** | | `false` | Shows the back button which triggers **onPressClose** |

#### I18n
```js
search: 'Search',
notfound: 'No Emoji Found',
categories: {
  search: 'Search Results',
  recent: 'Frequently Used',
  people: 'Smileys & People',
  nature: 'Animals & Nature',
  foods: 'Food & Drink',
  activity: 'Activity',
  places: 'Travel & Places',
  objects: 'Objects',
  symbols: 'Symbols',
  flags: 'Flags',
  custom: 'Custom',
}
```

#### Sheet sizes
Sheets are served from [unpkg](https://unpkg.com), a global CDN that serves files published to [npm](https://www.npmjs.com).

| Set       | Size (`sheetSize: 16`) | Size (`sheetSize: 20`) | Size (`sheetSize: 32`) | Size (`sheetSize: 64`) |
| --------- | ---------------------- | ---------------------- | ---------------------- | ---------------------- |
| apple     | 334 KB                 | 459 KB                 | 1.08 MB                | 2.94 MB                |
| emojione  | 315 KB                 | 435 KB                 | 1020 KB                | 2.33 MB                |
| facebook  | 322 KB                 | 439 KB                 | 1020 KB                | 2.50 MB                |
| google    | 301 KB                 | 409 KB                 |  907 KB                | 2.17 MB                |
| messenger | 325 KB                 | 449 MB                 | 1.05 MB                | 2.69 MB                |
| twitter   | 288 KB                 | 389 KB                 |  839 KB                | 1.82 MB                |

#### Datasets
While all sets are available by default, you may want to include only a single set data to reduce the size of your bundle.

| Set       | Size (on disk) |
| --------- | -------------- |
| all       | 570 KB         |
| apple     | 484 KB         |
| emojione  | 485 KB         |
| facebook  | 421 KB         |
| google    | 483 KB         |
| messenger | 197 KB         |
| twitter   | 484 KB         |

To use these data files (or any other custom data), use the `NimblePicker` component:

```js
import data from 'emoji-mart-native/data/messenger.json'
import { NimblePicker } from 'emoji-mart-native'

<NimblePicker set='messenger' data={data} />
```

#### Local image requires
By default the picker source the emoji images online, this may not be the best solution and you may want to bundle the emojis with your app.

| Set       | Size (on disk) |
| --------- | -------------- |
| all       | 1,2 MB         |
| apple     | 594 KB         |
| emojione  | 607 KB         |
| facebook  | 513 KB         |
| google    | 596 KB         |
| messenger | 270 KB         |
| twitter   | 602 KB         |

To use these requires files, you need to download the sets you want, as well as the `img-set-64` folder from https://github.com/iamcal/emoji-data and add them to your project. (for example assets/emojis). Usage:

```js
import data from 'emoji-mart-native/data/messenger.json'
import { NimblePicker } from 'emoji-mart-native'
import dataRequires from '/assets/emojis/messenger'

const {emojis: localEmojis} = dataRequires

<NimblePicker set='messenger' data={data} useLocalImages={localEmojis} />
```

#### Examples of `emoji` object:
```js
{
  id: 'smiley',
  name: 'Smiling Face with Open Mouth',
  colons: ':smiley:',
  text: ':)',
  emoticons: [
    '=)',
    '=-)'
  ],
  skin: null,
  native: '😃'
}

{
  id: 'santa',
  name: 'Father Christmas',
  colons: ':santa::skin-tone-3:',
  text: '',
  emoticons: [],
  skin: 3,
  native: '🎅🏼'
}

{
  id: 'octocat',
  name: 'Octocat',
  colons: ':octocat',
  text: '',
  emoticons: [],
  custom: true,
  imageUrl: 'https://assets-cdn.github.com/images/icons/emoji/octocat.png?v7'
}

```

### ModalPicker
Renders the picker in a fullscreen modal.

```jsx
import { ModalPicker } from 'emoji-mart-native'

<ModalPicker isVisible={true} showBackButton />
```

| Prop | Required | Default | Description |
| ---- | :------: | ------- | ----------- |
| **...PickerProps** | | | |
| **isVisible** | | `false` | When true shows the modal with the picker |

### Emoji
```jsx
import { Emoji } from 'emoji-mart-native'

<Emoji emoji={{ id: 'santa', skin: 3 }} size={16} />
<Emoji emoji=':santa::skin-tone-3:' size={16} />
<Emoji emoji='santa' set='emojione' size={16} />
```

| Prop | Required | Default | Description |
| ---- | :------: | ------- | ----------- |
| **emoji** | ✓ | | Either a string or an `emoji` object |
| **size** | ✓ | | The emoji width and height. |
| **native** | | `false` | Renders the native unicode emoji |
| **onClick** | | | Params: `(emoji, event) => {}` |
| **onLeave** | | | Params: `(emoji, event) => {}` |
| **onOver** | | | Params: `(emoji, event) => {}` |
| [**fallback**](#unsupported-emojis-fallback) | | | Params: `(emoji) => {}` |
| **set** | | `apple` | The emoji set: `'apple', 'google', 'twitter', 'emojione'` |
| **sheetSize** | | `64` | The emoji [sheet size](#sheet-sizes): `16, 20, 32, 64` |
| **backgroundImageFn** | | ```((set, sheetSize) => `https://unpkg.com/emoji-datasource@3.0.0/sheet_${set}_${sheetSize}.png`)``` | A Fn that returns that image sheet to use for emojis. Useful for avoiding a request if you have the sheet locally. |
| **skin** | | `1` | Skin color: `1, 2, 3, 4, 5, 6` |
| **tooltip** | | `false` | Show emoji short name when hovering (title) |
| [**html**](#using-with-dangerouslysetinnerhtml) | | `false` | Returns an HTML string to use with `dangerouslySetInnerHTML` |

#### Unsupported emojis fallback
Certain sets don’t support all emojis (i.e. Messenger & Facebook don’t support `:shrug:`). By default the Emoji component will not render anything so that the emojis’ don’t take space in the picker when not available. When using the standalone Emoji component, you can however render anything you want by providing the `fallback` props.

To have the component render `:shrug:` you would need to:

```js
<Emoji
  set={'messenger'}
  emoji={'shrug'}
  size={24}
  fallback={(emoji) => {
    return `:${emoji.short_names[0]}:`
  }}
/>
```

## Custom emojis
You can provide custom emojis which will show up in their own category.

```js
import { Picker } from 'emoji-mart-native'

const customEmojis = [
  {
    name: 'Octocat',
    short_names: ['octocat'],
    text: '',
    emoticons: [],
    keywords: ['github'],
    imageUrl: 'https://assets-cdn.github.com/images/icons/emoji/octocat.png?v7'
  },
]

<Picker custom={customEmojis} />
```

## Headless search
The `Picker` doesn’t have to be mounted for you to take advantage of the advanced search results.

```js
import { emojiIndex } from 'emoji-mart-native'

emojiIndex.search('christmas').map((o) => o.native)
// => [🎄, 🎅🏼, 🔔, 🎁, ⛄️, ❄️]
```

### With custom data
```js
import data from 'emoji-mart-native/datasets/messenger'
import { NimbleEmojiIndex } from 'emoji-mart-native'

let emojiIndex = new NimbleEmojiIndex(data)
emojiIndex.search('christmas')
```

## Storage
By default EmojiMartNative will store user chosen skin and frequently used emojis in `localStorage`. That can however be overwritten should you want to store these in your own storage.

```js
import { store } from 'emoji-mart-native'

store.setHandlers({
  getter: (key) => {
    // Get from your own storage (sync)
  },

  setter: (key, value) => {
    // Persist in your own storage (can be async)
  }
})
```

Possible keys are:

| Key | Value | Description |
| --- | ----- | ----------- |
| skin | `1, 2, 3, 4, 5, 6` | |
| frequently | `{ 'astonished': 11, '+1': 22 }` | An object where the key is the emoji name and the value is the usage count |
| last | 'astonished' | (Optional) Used by `frequently` to be sure the latest clicked emoji will always appear in the “Recent” category |

## Features
### Powerful search
#### Short name, name and keywords
Not only does **Emoji Mart Native** return more results than most emoji picker, they’re more accurate and sorted by relevance.

<img width="338" alt="summer" src="https://user-images.githubusercontent.com/12134822/40007143-ef8196be-5793-11e8-83ab-96373b0101ff.png">

#### Emoticons
The only emoji picker that returns emojis when searching for emoticons.

<img width="338" alt="emoticons" src="https://user-images.githubusercontent.com/12134822/40007146-f1c9d544-5793-11e8-9c0a-5b7767b7045b.png">

#### Results intersection
For better results, **Emoji Mart Native** split search into words and only returns results matching both terms.

<img width="338" alt="hand-raised" src="https://user-images.githubusercontent.com/12134822/40007148-f358a962-5793-11e8-951b-4c5a7c583f27.png">

### Fully customizable
#### Anchors color, title and default emoji
<img width="338" alt="customizable-color" src="https://user-images.githubusercontent.com/12134822/40007153-f56680ee-5793-11e8-9795-32fb54aa918f.png">

#### Emojis sizes and length
<img width="296" alt="size-and-length" src="https://user-images.githubusercontent.com/436043/32532590-381f67de-c400-11e7-86f6-328e30d6b116.png">

#### Default skin color
As the developer, you have control over which skin color is used by default.

<img width="205" alt="skins" src="https://user-images.githubusercontent.com/436043/32532858-0a559560-c402-11e7-8680-f77f780a5a49.png">

It can however be overwritten as per user preference.

<img width="98" alt="customizable-skin" src="https://user-images.githubusercontent.com/436043/32532883-2c620e7c-c402-11e7-976c-50d32be0566c.png">

#### Multiple sets supported
Apple / Google / Twitter / EmojiOne / Messenger / Facebook

<img width="214" alt="sets" src="https://user-images.githubusercontent.com/436043/33786868-d4226e60-dc38-11e7-840a-e4cf490f5f4a.png">

## Not opinionated
**Emoji Mart Native** doesn’t automatically insert anything into a text input, nor does it show or hide itself. It simply returns an `emoji` object. It’s up to the developer to mount/unmount (it’s fast!) and position the picker. You can use the returned object as props for the `EmojiMartNative.Emoji` component. You could also use `emoji.colons` to insert text into a textarea or `emoji.native` to use the emoji.

## Development
```sh
$ yarn build
$ yarn start
$ yarn storybook
```

To easier test changes as you make them, you can run `npm run build:link -- --out-dir /$project/node_modules/emoji-mart-native/dist` replacing `$project` with your projects location.

## 🎩 Hat tips!
Ported from code brought to you by the <a title="Team email, team chat, team tasks, one app" href="https://missiveapp.com">Missive</a> team<br>
Powered by [iamcal/emoji-data](https://github.com/iamcal/emoji-data) and inspired by [iamcal/js-emoji](https://github.com/iamcal/js-emoji).<br>
🙌🏼  [Cal Henderson](https://github.com/iamcal).
