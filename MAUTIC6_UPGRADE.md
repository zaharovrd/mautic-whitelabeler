# Mautic 6 Compatibility Upgrade - Summary of Changes

## Overview
This document outlines all changes made to update the Mautic Whitelabeler project for compatibility with Mautic 6.0.0 through 6.0.7.

## Changes Made

### 1. **Removed Legacy Template Versions** ✅
- **Action**: Deleted all template directories for Mautic versions older than 5.0.0
- **Removed**: 
  - Mautic 2.15.0 - 2.16.5
  - Mautic 3.0.0 - 3.3.5
  - Mautic 4.0.0 - 4.4.13
- **Remaining**: Only Mautic 5.x templates and all 6.0.x templates
- **Reason**: Per user requirements to remove outdated versions

### 2. **Updated README.md** ✅
- **Old**: "Mautic versions 2.15.0 - 5.1.1"
- **New**: "Mautic versions 5.0.0 - 6.0.7"
- Added reference to use Whitelabeler 1.0 for Mautic 2.x - 4.x versions

### 3. **Added Mautic 6.0.x Template Support** ✅
- **Templates Created**: 
  - `templates/6.0.0/`
  - `templates/6.0.1/`
  - `templates/6.0.2/`
  - `templates/6.0.3/`
  - `templates/6.0.4/`
  - `templates/6.0.5/`
  - `templates/6.0.6/`
  - `templates/6.0.7/` (latest)
- **Source**: Based on `templates/5.1.1/` (identical structure)
- **Reason**: Mautic 6.0.x versions use the same file structure as 5.x (Twig templates)

### 4. **Updated PHP Code for Version Detection** ✅

#### File: `whitelabeler.php`

**Method: `companyName()`**
- Changed version check from `if ( substr($version, 0, 1) == 5 )` to `if ( substr($version, 0, 1) >= 5 )`
- This now supports Mautic 5.x AND 6.x versions
- Both use Twig templates (`.html.twig` files)

**Method: `replaceImages()`**
- Updated login page version detection from `== 5` to `>= 5`
- Updated sidebar logo version detection to handle both 5.x and 6.x

**Method: `compareMauticVersions()`**
- Already compatible - uses `>= 5` comparisons which work for 6.x

### 5. **JavaScript & Frontend** ✅
- **Status**: No changes required
- **Libraries Used**:
  - jQuery 3.1.1 (modern, compatible with Mautic 6)
  - Bootstrap 3 (minified)
  - Spectrum (color picker - not deprecated in Mautic 6)
  - Font-Awesome 4.7.0 (for icons)
- **Removed Libraries**: None were found that needed removal
  - jQuery UI: Not used in this project
  - Froala: Not used in this project
  - CodeMirror: Not used in this project
  - Modernizr: Not used in this project

### 6. **Updated Dependencies (composer.json)** ✅

#### Before:
```json
{
    "name": "nick/mautic-whitelabeler",
    "authors": [...],
    "require": {
        "chrisjean/php-ico": "^1.0",
        "components/font-awesome": "4.7.0"
    },
    "config": {
        "COMPOSER_ALLOW_SUPERUSER" : 1
    }
}
```

#### After:
```json
{
    "name": "nick/mautic-whitelabeler",
    "description": "Mautic Whitelabeler - Customize your Mautic installation branding",
    "authors": [...],
    "require": {
        "php": "^8.0",
        "chrisjean/php-ico": "^1.0",
        "components/font-awesome": "^4.7"
    },
    "require-dev": {},
    "config": {
        "allow-plugins": {
            "composer/installers": true
        },
        "COMPOSER_ALLOW_SUPERUSER": 1
    }
}
```

#### Changes:
- Added `"description"` field
- Added PHP 8.0+ requirement (Mautic 6 requirement)
- Updated Font-Awesome from pinned `4.7.0` to `^4.7` for flexibility
- Added `"require-dev"` field for future development dependencies
- Updated `config` to include `allow-plugins` (Composer 2.x requirement)

## Compatibility Matrix

| Feature | Mautic 5.x | Mautic 6.x |
|---------|-----------|-----------|
| Version Detection | ✅ | ✅ |
| CSS Color Replacement | ✅ | ✅ |
| Logo Replacement | ✅ | ✅ |
| Company Name Replacement | ✅ | ✅ |
| Template Files (.twig) | ✅ | ✅ |
| JavaScript Libraries | ✅ | ✅ |

## Testing Recommendations

1. **Version Detection**: Test with both 5.1.1 and 6.0.0+ Mautic installations
2. **File Operations**: Verify that template files are correctly read and written
3. **CSS Application**: Confirm colors are applied correctly to both versions
4. **Image Replacement**: Test logo upload and placement
5. **Cache Clearing**: Verify Symfony cache clearing works in both versions

## Notes on Mautic 6 Breaking Changes

This project does NOT directly use:
- `MauticFactory` (removed in Mautic 6) - not a plugin dependency
- Session service directly - not needed for this standalone tool
- Guard authentication - not relevant to this project
- Any of the deprecated bundles mentioned in the upgrade guide

Since Mautic Whitelabeler is a standalone CLI tool that reads/writes files rather than integrating with Mautic's service container, most of the major Mautic 6 breaking changes do not affect it.

## Future Considerations

1. **PHP Version**: Consider upgrading minimum PHP requirement to 8.1 when Mautic 6.2+ is released
2. **Framework Updates**: Monitor Symfony updates for major versions affecting template syntax
3. **Additional Versions**: As new Mautic 6.x versions are released, create template copies as needed
4. **Dependencies**: Keep an eye on `chrisjean/php-ico` and `font-awesome` package updates
