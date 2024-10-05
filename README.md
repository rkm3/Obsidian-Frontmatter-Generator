# Obsidian frontmatter generator

Generate your frontmatter on save.

✅ Powerful, dead simple

## Usage

1. After installing the plugin, visit the setting of the plugin
2. Change the frontmatter template

For example, the following frontmatter template

```ts
{
 folder: file.parent.path,
 title: file.basename,
 test: ["1", "2"]
}
```

will generate this in the file `Good recipes/scrambled egg.md` on save.

```yaml
folder: Good recipes
title: scrambled egg
test:
  - '1'
  - '2'
```

3. Install the plugin [obsidian-custom-save](https://github.com/HananoshikaYomaru/obsidian-custom-save) and add the `frontmatter-generator: run file` command to the custom save actions

- Basic Demo: <https://youtu.be/Cz9d5e1WQVM>
- Tag properties demo: <https://www.youtube.com/watch?v=lyhrOG2Sn88&t=16>

## Advanced usage

### Conditional expressions

```ts
file.properties?.type === 'kanban'
 ? {
   folder: file.parent.path,
   title: file.basename
   }
 : {}
```

### Functions

```ts
{
 test: (() => {
  return { test: 'test' }
 })()
}
```

### Dataview

```ts
{
 numberOfPages: dv.pages('#ai').length
}
```

## Syntax of the frontmatter template

It could be a json or a javascript expression that returns an object.

![](https://share.cleanshot.com/nfW5nV8L+)

<small>^ even functions work</small>

## Variables that it can access

- `file`, the [`TFile`](https://docs.obsidian.md/Reference/TypeScript+API/TFile/TFile) object
- `file.properties` will access the yaml object of the current file
- `file.tags` , a `string[]` which will access the tags of the current file. For example `["#book", "#movie"]`
- `dv`, the [dataview](https://blacksmithgu.github.io/obsidian-dataview/) object (you can only access this if you install and enable the Dataview plugin)
- `z`, the zod object

## Installation

### Install from the Obsidian plugin marketplace

You can find it on Obsidian plugin marketplace.

### Manual Installation

1. `cd` to `.obsidian/plugins`
2. `git clone` this repo
3. `cd obsidian-frontmatter-generator && bun install && bun run build`
4. there you go 🎉

## Notes

1. To stop generate on a file, you can put `yaml-gen-ignore: true` in the frontmatter. You can also ignore the whole folder in the setting.
2. The context that you can access is [TFile](https://docs.obsidian.md/Reference/TypeScript+API/TFile/TFile). This can be updated in the future. It is extremely flexible.
3. This plugin also comes with some commands to run in folder and in the whole vault.
4. If you want to contribute, first open an issue.
5. 🚨 This plugin is still under development, don't try to hack it by using weird keywords or accessing global variables in the template. It should not work but if you figure out a way to hack it, it will just break your own vault.

<!--
## How to release

```
# update the version number in package.json
bun version
git add .
git commit -m <message>
git tag -a <version> -m <version>
git push origin <version>
git push
# after the release workflow done, update the release doc on github
```

 -->
