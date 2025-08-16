# SelectJS ⚡

A powerful, lightweight, and highly customizable JavaScript library that transforms HTML select elements into modern, searchable dropdowns with mobile-responsive design.

> ⚠️ **Development Status**: This project is currently in active development. This is the initial MVP (Minimum Viable Product) release. Features may change and additional functionality will be added in future versions.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Version](https://img.shields.io/badge/version-1.0.0--MVP-orange.svg)
![Status](https://img.shields.io/badge/status-in%20development-yellow.svg)
![Size](https://img.shields.io/badge/size-~15kb-orange.svg)
![Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen.svg)

## ✨ Features

- 🔍 **Search functionality** - Filter options as you type
- 📱 **Mobile responsive** - Automatic modal interface for mobile devices
- 🎨 **Highly customizable** - Easy styling and theming
- 🚀 **Zero dependencies** - Pure JavaScript implementation
- ♿ **Accessibility friendly** - Proper ARIA attributes and keyboard navigation
- 🏷️ **Optgroup support** - Organize options with groups
- 📋 **Form integration** - Works seamlessly with forms and validation
- 🎯 **Event handling** - Custom events for interaction tracking
- 🔧 **API methods** - Programmatic control over select elements

## 🚀 Quick Start

### 🚀 Installation

#### 📦 Via CDN (Recommended)

```html
<script src="https://cdn.jsdelivr.net/gh/pedrohrigolin/select-js@MVP1.0.0/selectJS.min.js"></script>
```

#### 📥 Local Download

```html
<script src="path/to/selectJS.js"></script>
```

> 💡 **Note:** The library includes all necessary CSS styles. No additional external files required.

---

### Basic Usage

1. **HTML Structure**
```html
<select class="selectJS" name="country">
  <option value="us">United States</option>
  <option value="ca">Canada</option>
  <option value="uk">United Kingdom</option>
</select>
```

2. **Initialize**
```javascript
// Initialize all select elements with class 'selectJS'
selectJS.all();

// Or initialize a specific element
const mySelect = document.querySelector('#my-select');
selectJS.element(mySelect);
```

## 📚 API Reference

### 🔧 Initialization Methods

#### `selectJS.all()`
Transforms all select elements with class `selectJS` into SelectJS components.

#### `selectJS.element(selectElement)`
Transforms a specific select element into a SelectJS component.

**Parameters:**
- `selectElement` (HTMLSelectElement) - The select element to transform

### 🎨 Styling Methods

#### `selectJS.setStyle(cssString)`
Replaces the default styles with custom CSS.

```javascript
selectJS.setStyle(`
  .selectJS {
    width: 300px;
    font-family: Arial, sans-serif;
  }
  .selectJS-searchInput {
    padding: 15px;
    border-radius: 10px;
  }
`);
```

#### `selectJS.addStyle(cssString)`
Adds additional CSS rules to the existing styles.

```javascript
selectJS.addStyle(`
  .selectJS-option:hover {
    background-color: #e3f2fd;
  }
`);
```

### ⚙️ Control Methods

#### `selectJS.disable(selectElement)`
Disables a SelectJS component.

#### `selectJS.enable(selectElement)`
Enables a previously disabled SelectJS component.

#### `selectJS.required(selectElement, state)`
Sets or removes the required attribute.

**Parameters:**
- `selectElement` (HTMLDivElement) - The SelectJS component
- `state` (boolean) - True to make required, false to remove

#### `selectJS.readonly(selectElement, state)`
Sets or removes the readonly attribute.

### 📊 Value Management

#### `selectJS.setValue(selectElement, value)`
Programmatically sets the value of a SelectJS component.

```javascript
const mySelect = document.querySelector('.selectJS');
selectJS.setValue(mySelect, 'us');
```

#### `selectJS.getValue(selectElement)`
Gets the current value of a SelectJS component.

```javascript
const value = selectJS.getValue(mySelect);
console.log(value); // 'us'
```

#### `selectJS.getAllValues(options)`
Retrieves values from all SelectJS components on the page.

```javascript
// Get all values using 'name' attribute as key
const values = selectJS.getAllValues();

// Get all values using 'id' attribute as key
const valuesById = selectJS.getAllValues({ keyType: 'id' });

// Get all values with complete information
const allData = selectJS.getAllValues({ includeAll: true });
```

**Parameters:**
- `options.keyType` (string) - 'name' or 'id' (default: 'name')
- `options.includeAll` (boolean) - Return complete object with id, name, and value (default: false)

## 🎯 Events

SelectJS dispatches custom events for better integration:

### `create`
Fired when a SelectJS component is created.

```javascript
document.addEventListener('create', function(e) {
  console.log('SelectJS created:', e.target);
});
```

### `selectJS.change`
Fired when the value changes, providing both old and new values.

```javascript
document.addEventListener('selectJS.change', function(e) {
  console.log('Value changed from', e.detail.oldValue, 'to', e.detail.newValue);
  console.log('Target:', e.detail.target);
  console.log('Input:', e.detail.input);
});
```

## 🏗️ Advanced Usage

### HTML Attributes

SelectJS supports various HTML attributes for enhanced functionality:

```html
<select class="selectJS" 
        name="country" 
        placeholder="Choose a country..."
        selectJS-id="country-select"
        selectJS-modalID="country-modal"
        selectJS-modalBoxID="country-modal-box"
        required>
  <optgroup label="North America">
    <option value="us">United States</option>
    <option value="ca">Canada</option>
  </optgroup>
  <optgroup label="Europe">
    <option value="uk" selected>United Kingdom</option>
    <option value="fr">France</option>
    <option value="de" default>Germany</option>
  </optgroup>
</select>
```

**Supported Attributes:**
- `name` - Form field name
- `placeholder` - Placeholder text for search input
- `selectJS-id` - Custom ID for the hidden input
- `selectJS-modalID` - Custom ID for mobile modal
- `selectJS-modalBoxID` - Custom ID for modal content box
- `required` - Makes the field required
- `disabled` - Disables the select
- `readonly` - Makes the select readonly
- `selected` - Marks an option as selected
- `default` - Sets a default fallback option

### Working with Forms

SelectJS integrates seamlessly with HTML forms:

```html
<form id="user-form">
  <select class="selectJS" name="country" required>
    <option value="us">United States</option>
    <option value="ca">Canada</option>
  </select>
  
  <button type="submit">Submit</button>
</form>
```

```javascript
selectJS.all();

document.getElementById('user-form').addEventListener('submit', function(e) {
  e.preventDefault();
  
  const formData = new FormData(this);
  console.log('Country:', formData.get('country'));
});
```

### Mobile Responsiveness

SelectJS automatically detects mobile devices and switches to a modal interface for better user experience on small screens.

## 🎨 Customization

### CSS Classes

SelectJS uses the following CSS classes that you can customize:

- `.selectJS` - Main container
- `.selectJS-searchInput` - Search/display input
- `.selectJS-container` - Dropdown container
- `.selectJS-option` - Individual options
- `.selectJS-optgroup` - Option groups
- `.selectJS-optgroupTitle` - Option group titles
- `.selectJS-modal` - Mobile modal backdrop
- `.selectJS-modalBox` - Mobile modal content
- `.selectJS-modalSearchInput` - Mobile search input
- `.selectJS-modalOption` - Mobile modal options

### Custom Themes

Create beautiful themes by customizing the CSS:

```javascript
selectJS.setStyle(`
  /* Dark theme example */
  .selectJS-searchInput {
    background-color: #2d2d2d;
    color: #ffffff;
    border: 1px solid #555;
  }
  
  .selectJS-option {
    background-color: #2d2d2d;
    color: #ffffff;
  }
  
  .selectJS-option:hover {
    background-color: #404040;
  }
`);
```

## 🌐 Browser Support

SelectJS works in all modern browsers:

- ✅ Chrome 60+
- ✅ Firefox 55+
- ✅ Safari 11+
- ✅ Edge 79+
- ✅ Mobile browsers

## 📱 Mobile Features

- **Automatic detection** of mobile devices
- **Modal interface** for better touch interaction
- **Large touch targets** for easy selection
- **Full-screen search** on mobile devices

## ⚡ Performance

- **Lightweight** - Only ~15KB minified
- **No dependencies** - Pure JavaScript
- **Efficient rendering** - Virtual scrolling for large datasets
- **Memory optimized** - Proper cleanup and event management

## 🚧 Development Roadmap

As this is an MVP release, here are some planned features for future versions:

- 🔄 **Enhanced keyboard navigation** (Arrow keys, Enter, Escape)
- 🎯 **Multiple selection support** 
- 🌍 **Internationalization (i18n)** support
- 🎨 **Built-in themes** (Dark, Light, Material, etc.)
- ⚡ **Virtual scrolling** for large datasets
- 🔌 **Plugin system** for extensions
- 📊 **Better accessibility** features
- 🧪 **Unit tests** and documentation improvements

## 🤝 Contributing

Contributions are welcome! Since this project is in active development, please feel free to:

- 🐛 Report bugs and issues
- 💡 Suggest new features
- 📝 Improve documentation
- 🔧 Submit Pull Requests

**Getting Started:**
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

> **Note:** As this is an MVP, breaking changes may occur between versions until we reach a stable 1.0.0 release.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Pedro Rigolin**
- GitHub: [@pedrohrigolin](https://github.com/pedrohrigolin)

## 🙏 Acknowledgments

- Inspired by the need for better select elements in modern web applications
- Built with mobile-first approach in mind
- Special thanks to the web development community for feedback and suggestions

---

⭐ **Star this repository if you find it helpful!**
