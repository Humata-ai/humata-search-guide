
# Humata Search Guide

This guide provides a explanation of how to initialize and use the Humata Search. It includes information on configuring filters, setting up localization, and interacting with the search programmatically.

### Initializing Humata Search
```html
// Styles
<link
      rel="stylesheet"
      href="https://ylxjwvrtrrjvefpnlfln.supabase.co/storage/v1/object/public/humata-search/styles.css"
    />

```

```js
const scriptEl = document.createElement("script");
scriptEl.src =
        "https://ylxjwvrtrrjvefpnlfln.supabase.co/storage/v1/object/public/humata-search/widget.js";
scriptEl.onload = ()=>{
    const humataSearch = new HumataSearch("<ConfigurationID>",{
    tags, // Filter tags for the Rag navigator.
    langs, // Languages object for the localization
    inputContainer:"#input-container", // HMTL element's query selector to render the input component
    container:"#container" // HTML element's query selector to render the humata search
});
}

```
### Search Filters
The Humata search uses the `tags` object provided during initialization to generate RAG Navigator's search filters.
```js
//English
const tags = {
        category: [
          { label: 'Regulations', value: 'Regulations' },
          { label: 'Guidelines', value: 'Guidelines' },
          { label: 'E-Services', value: 'E-Services' },
        ],
        area: [
          { label: 'Value Added Tax', value: 'Value Added Tax' },
          { label: 'Zakat', value: 'Zakat' },
          { label: 'Customs', value: 'Customs' },
          { label: 'Corporate IT', value: 'Corporate IT' },
          { label: 'Real Estate Tax', value: 'Real Estate Tax' },
          { label: 'Excise Tax', value: 'Excise Tax' },
          { label: 'Transfer Pricing', value: 'Transfer Pricing' },
          { label: 'FATCA', value: 'FATCA' },
          { label: 'E-Invoice', value: 'E-Invoice' },
          { label: 'General', value: 'General' },
        ],
      };
      
// Arabic
const tags = {
        category: [
          { label: 'اللوائح التنظيمية', value: 'اللوائح التنظيمية' },
          { label: 'الإرشادات', value: 'الإرشادات' },
          { label: 'الخدمات الإلكترونية', value: 'الخدمات الإلكترونية' },
        ],
        area: [
          { label: 'الزكاة', value: 'الزكاة' },
          { label: 'الجمارك', value: 'الجمارك' },
          { label: 'تقنية المعلومات المؤسسية', value: 'تقنية المعلومات المؤسسية' },
          { label: 'الضريبة العقارية', value: 'الضريبة العقارية' },
          { label: 'ضريبة القيمة المضافة', value: 'ضريبة القيمة المضافة' },
          { label: 'ضريبة السلع الانتقائية', value: 'ضريبة السلع الانتقائية' },
          { label: 'تسعير المعاملات', value: 'تسعير المعاملات' },
          { label: 'فاتكا', value: 'فاتكا' },
          { label: 'الفاتورة الإلكترونية', value: 'الفاتورة الإلكترونية' },
          { label: 'عام', value: 'عام' },
        ],
      };
```

### Localization
The Humata Search uses i18n to handle localization. To add translations you can use `langs` object.

```js
// Arabic translations
      const langs = {
        ar: {
          input: {
            placeholder: 'ماذا تريد أن تبحث عنه؟',
            buttons: { ask_ai: 'اسأل زياد', regulations: 'الأنظمة والتشريعات', stop: 'Stop generating' },
          },
          preview: { view_doc: 'View doc' },
          search: {
            results: {
              count: 'النتائج',
              page: 'Page',
              no_results: 'لم يتم العثور على نتائج',
              filters: {
                area: 'نوع',
                sort: 'فئة',
                category: 'منطقة',

                placeholders: { category: 'الكل', area: 'الكل' },
                sort_most_relevant: 'الأكثر صلة',
                sort_alphabetical: 'أبجديا',
              },
              buttons: {
                download: 'Download',
                ask_ai: 'Ask AI',
              },
            },
          },
        },
      };
```

By default, Humata Search uses `en` as the default locale. You can change the locale with this function;
```js
humataSearch.setLocale('ar');
```

### Setting search query programmatically
You can use this function to set the input component's query value, for example, when a user clicks a suggested question.
```js
humataSearch.setQuery("Your query");
```

### Document preview 
The Humata search's container should have a maximum height to prevent PDF files from overflowing; otherwise, the rendering and auto-scrolling behavior might not work.

### Hiding the Humata Search
Sometimes you may want to hide the Humata Search (except the input component); in that case, you can use the following function:
```js
humataSearch.hide();
```
