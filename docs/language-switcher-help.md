# Ensuring that the English and Irish (Gaelic) versions of your content are correctly identified

Ensuring that the English and Irish (Gaelic) versions of your content are correctly identified as translations of each other is crucial for a seamless multilingual experience on your Hugo site. Even if the titles differ between languages, Hugo provides mechanisms to link translated content.

### **Understanding Hugo's Translation Mechanism**

Hugo identifies translations of content based on:

1. **File Naming Conventions**
2. **Front Matter Parameters**

Let's explore how to use these methods to link your English and Irish versions.

---

### **1. Using File Naming Conventions**

#### **a. Consistent Filenames Across Languages**

Hugo associates translated content when the filenames (excluding the language code or extension) are the same. Even if the titles differ, the base filename should be consistent.

**Example:**

- English content file: `chapter1.md`
- Irish content file: `chapter1.md`

**Directory Structure:**

```
content/
  en/
    the_corpse/
      chapter1.md
  ga/
    the_corpse/
      chapter1.md
```

#### **b. Language Code Suffixes (Optional)**

If you prefer to keep all content in a single directory, you can use language code suffixes in filenames.

**Example:**

- English file: `chapter1.en.md`
- Irish file: `chapter1.ga.md`

**But since you're using separate directories for each language, you can omit the language code suffixes.**

---

### **2. Using Front Matter Parameters**

When titles differ or when you need explicit control, you can use the `translationKey` parameter in the front matter to link content.

#### **a. Add `translationKey` to Front Matter**

Assign a unique `translationKey` to each piece of content that should be linked across languages.

**English `chapter1.md`:**

```markdown
---
title: "Chapter 1: The Beginning"
translationKey: "chapter1"
weight: 1
---
```

**Irish `chapter1.md`:**

```markdown
---
title: "Caibidil 1: An Tosú"
translationKey: "chapter1"
weight: 1
---
```

#### **Explanation:**

- **`translationKey`**: A unique identifier that Hugo uses to link translations.
- **Titles**: Can be different in each language.

#### **b. Consistency of `translationKey`**

Ensure the `translationKey` is identical in all language versions of the content.

---

### **3. Configuring Hugo for Multilingual Linking**

#### **a. Verify Language Settings in `hugo.toml`**

Your `hugo.toml` should already have the multilingual configuration:

```toml
defaultContentLanguage = "en"
defaultContentLanguageInSubdir = true

[languages]
  [languages.en]
    languageName = "English"
    weight = 1
    contentDir = "content/en"
  [languages.ga]
    languageName = "Irish"
    weight = 2
    contentDir = "content/ga"
```

#### **b. Set `enableMissingTranslationPlaceholders` (Optional)**

For debugging purposes, you can enable placeholders to identify missing translations.

```toml
enableMissingTranslationPlaceholders = true
```

---

### **4. Implementing Language Switcher in the Theme**

To allow users to switch between English and Irish versions of a page, you need to ensure the theme supports language switching.

#### **a. Check Theme Support**

The `hugo-book` theme supports multilingual sites and can display a language switcher if configured correctly.

#### **b. Enable Language Switcher**

In your `hugo.toml`, add or update the `[params]` section:

```toml
[params]
  rootPage = ""
  disableSearch = false
  BookToC = true
  disableLanguageSwitchingButton = false  # Ensure this is set to false
```

#### **c. Adjust Theme Templates (If Necessary)**

If the language switcher doesn't appear, you may need to adjust the theme's templates.

- **Locate the Language Switcher Partial:**

  The language switcher is typically defined in `themes/hugo-book/layouts/partials/navbar.html` or a similar file.

- **Ensure the Partial Includes the Switcher Logic:**

  The partial should include code that generates the language switcher based on available translations.

---

### **5. Example of Content Files with `translationKey`**

**English Content: `content/en/the_corpse/chapter1.md`**

```markdown
---
title: "Chapter 1: The Beginning"
translationKey: "chapter1"
weight: 1
---

# Chapter 1: The Beginning

Content of Chapter 1 in English.
```

**Irish Content: `content/ga/the_corpse/chapter1.md`**

```markdown
---
title: "Caibidil 1: An Tosú"
translationKey: "chapter1"
weight: 1
---

# Caibidil 1: An Tosú

Ábhar Caibidil 1 i nGaeilge.
```

---

### **6. Testing the Setup**

#### **a. Start the Hugo Server**

Run the development server to test the site:

```bash
hugo server -D
```

#### **b. Navigate to a Page**

- **English Version:** `http://localhost:1313/en/the_corpse/chapter1/`
- **Irish Version:** `http://localhost:1313/ga/the_corpse/chapter1/`

#### **c. Verify Language Switching**

- On the English page, look for a language switcher (usually at the top or in the sidebar).
- Switch to the Irish version and verify that it displays the correct content.

---

### **7. Handling Different Titles in Navigation**

Even though the titles are different, the navigation should correctly display the titles in the respective languages.

#### **a. Sidebar Navigation**

The sidebar should list chapters using the `title` specified in each content file's front matter.

#### **b. Order of Items**

Use the `weight` parameter to order chapters consistently across languages.

---

### **8. Additional Tips**

#### **a. Consistent Filenames and Paths**

Ensure that the content files have the same relative paths and filenames in both languages.

- **Example:**

  - English: `content/en/the_corpse/chapter1.md`
  - Irish: `content/ga/the_corpse/chapter1.md`

#### **b. Multilingual Taxonomies (If Used)**

If you're using taxonomies (tags, categories), ensure they are translated appropriately.

- Define taxonomies per language in `hugo.toml` if necessary.

#### **c. Navigation Links**

If you manually create links within your content, use relative URLs to allow Hugo to handle the correct language paths.

---

### **9. Summary of Steps**

1. **Use Consistent Filenames:** Keep filenames the same across languages.
2. **Add `translationKey`:** Include a unique `translationKey` in the front matter of each content file.
3. **Set Up Language Switcher:** Configure the theme to display a language switcher.
4. **Test Thoroughly:** Run the site locally and verify that translations are linked correctly.
5. **Maintain Content Structure:** Ensure that the directory structure mirrors between languages.

---

### **10. Potential Issues and Solutions**

#### **Issue:** Language Switcher Not Appearing

- **Solution:** Verify that `disableLanguageSwitchingButton` is set to `false` in `[params]`.
- **Check Theme Compatibility:** Ensure the theme supports language switching and that you're using the latest version.

#### **Issue:** Translations Not Linked Correctly

- **Solution:** Double-check that the `translationKey` is identical in all language versions.
- **Consistent Filenames:** Ensure filenames match across languages.

#### **Issue:** Navigation Order Differs Between Languages

- **Solution:** Use the same `weight` values in the front matter for all language versions.

---

### **11. Example `hugo.toml` with All Settings**

```toml
baseURL = 'https://example.org/'
languageCode = 'en-us'
title = 'My Book Translations Site (English, Irish)'
theme = 'hugo-book'

defaultContentLanguage = "en"
defaultContentLanguageInSubdir = true
enableMissingTranslationPlaceholders = false

[params]
  rootPage = ""
  disableSearch = false
  BookToC = true
  disableLanguageSwitchingButton = false

[languages]
  [languages.en]
    languageName = "English"
    weight = 1
    contentDir = "content/en"
    [languages.en.params]
      rootPage = ""

  [languages.ga]
    languageName = "Irish"
    weight = 2
    contentDir = "content/ga"
    [languages.ga.params]
      rootPage = ""

[taxonomies]
  tag = "tags"
  category = "categories"
```

---

### **12. Conclusion**

By following these steps, you can ensure that Hugo correctly identifies and links the English and Irish versions of your content, even when the titles differ. The key is to maintain consistent filenames and use the `translationKey` in the front matter.

---

### **Need Further Assistance?**

If you have any questions or run into any issues:

- **Content Structure:** Share your directory structure and any specific files you're unsure about.
- **Configuration Details:** Provide snippets of your `hugo.toml` or front matter if you need clarification.
- **Theme Customization:** If the theme doesn't behave as expected, we can look into adjusting templates or parameters.

Feel free to ask for further clarification or assistance, and I'll be happy to help you get your multilingual Hugo site working perfectly!
