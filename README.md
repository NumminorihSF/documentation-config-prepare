# documentation-config-prepare

This is a small tool for prepare the documentation.js config from its part
that present in file tree. Wrote for `@saritasa/generator-react` and 
`react-app-core` so there is no customisation for current moment, but tool is pretty small,
so you may do PR or write your own.

## How to use
For single-time usage, you may run
```bash
npx documentation-config-prepare
```

For regular usage it's recommended to use
1. `npm install --save-dev documentation-config-prepare`
2. Create `predoc` script inside package.json like `"predoc": "documentation-config-prepare"`
3. If you run `npm run doc` for building the documentation, `predoc` runs before it

## What does it do
This tool use yaml files that named like `documentation.yml` or `MyModule.documentation.yml`,
where `MyModule` is custom part.

The algorithm is next:
1. Take all files by glob from `src` folder and remember theirs paths.
2. Parse paths to understand if documentation file were created for `feature` or not (looking for `/features/` in path).
3. Sort all files like:
```
file1
file2 <-- all files except features are sorted in alphabetical order 
file3
feature1 <-- after regular files, features goes (alphabetical order too)
feature2
feature2-file1 <-- every feature's regular file is placed rigth after main feature description 
feature2-file2 <-- (alphabetical order too)
feature2.1 (nested for feature2) <-- every nested feature goes after regular feature's files
feature2.2 (nested for feature2)
feature3
feature4
```
4. Take file's content from `toc` key and concat it with another.
5. Write `documentation.yml` into `process.cwd()`.