#php #symfony #bootstrap 

# Add Bootstrap to Symfony
## Add CSS
- Rename `assets/styles/app.css` to `app.scss`
- Import Bootstrap SCSS in `app.css`
```css
@import "~bootstrap/scss/bootstrap";
```
- Enable Sass Loader in `webpack.config.js` -> `.enableSassLoader()`
- Run `npm run build` to get the correct version of sass-loader to install
`npm install sass-loader@^12.0.0 sass --save-dev`
- Install postcss `npm install postcss-loader autoprefixer --dev`  
- Create `postcss.config.js` at the root of the project
```javascript
module.exports = { 
	plugins: { 
		autoprefixer: {} 
	} 
}
```

## Add JS
- Import bootstrap utilities in `app.js`
```javascript
import { Tooltip, Toast, Popover } from 'bootstrap';
```

**Along the steps, regularly run `ǹpm run build` to check everything is alright**