# Changelog

## [3.0.0] - 2025-01-14

### Added
- **Mautic 6.0.0+ Support**: Full compatibility with Mautic 6.0.0 through 6.0.7 versions
- New template directories: 
  - `templates/6.0.0/`
  - `templates/6.0.1/`
  - `templates/6.0.2/`
  - `templates/6.0.3/`
  - `templates/6.0.4/`
  - `templates/6.0.5/`
  - `templates/6.0.6/`
  - `templates/6.0.7/` (latest stable)
- PHP 8.0+ requirement in composer.json
- Project description in composer.json
- Composer 2.x plugin configuration support

### Changed
- Updated version detection in `companyName()` method to support Mautic 6.x
- Updated version detection in `replaceImages()` method to support Mautic 6.x
- Font-Awesome version constraint from pinned `4.7.0` to flexible `^4.7`
- Updated README.md to indicate support for Mautic 5.0.0 - 6.0.7

### Removed
- All template versions for Mautic 2.x (2.15.0 - 2.16.5)
- All template versions for Mautic 3.x (3.0.0 - 3.3.5)
- All template versions for Mautic 4.x (4.0.0 - 4.4.13)
- Legacy builder support references from documentation

### Deprecated
- Support for Mautic versions below 5.0.0 (use Whitelabeler 1.0 for older versions)

### Fixed
- Composer configuration warnings in modern Composer 2.x versions

### Technical Details
- Version detection now uses `>= 5` comparison for Twig template path selection
- Both Mautic 5.x and 6.x use identical template file structure
- No breaking changes to the public API
- Project remains a standalone CLI tool compatible with all versions
- Tested compatibility: 6.0.0, 6.0.1, 6.0.2, 6.0.3, 6.0.4, 6.0.5, 6.0.6, 6.0.7

### Known Limitations
- Mautic 6.0.x versions use the same template file structure, so templates are interchangeable
- Future Mautic 6.1+ versions may require template updates if core file structure changes

---

## [2.0.0] - Previous Release

Previous functionality for Mautic 2.15.0 - 5.1.1

### Features
- Command line whitelabeler
- Save/restore configurations
- Logo customization
- Color customization
- Company name replacement
- Footer customization
