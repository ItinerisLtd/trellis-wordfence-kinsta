# trellis-wordfence-kinsta

[![GitHub tag](https://img.shields.io/github/tag/ItinerisLtd/trellis-wordfence-kinsta.svg)](https://github.com/ItinerisLtd/trellis-wordfence-kinsta/tags)
[![license](https://img.shields.io/github/license/ItinerisLtd/trellis-wordfence-kinsta.svg)](https://github.com/ItinerisLtd/trellis-wordfence-kinsta/blob/master/LICENSE)

Ensure required WordfFence files exist in shared directory.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Requirements](#requirements)
- [Installation](#installation)
- [Role Variables](#role-variables)
- [Usage](#usage)
- [FAQs](#faqs)
  - [WordFence still complains that the firewall is not configured!](#wordfence-still-complains-that-the-firewall-is-not-configured)
- [Testing](#testing)
  - [Syntax Check](#syntax-check)
- [Author Information](#author-information)
- [Feedback](#feedback)
- [Change log](#change-log)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Requirements

- Trellis [6b40320](https://github.com/roots/trellis/commit/7cdfbde363b8f8b1947fbd4ea28ba31af2067f6d) or later
- Ansible v2.6 or later
- Bedrock
- WordFence

## Installation

Add this role to `galaxy.yml`:
```yaml
# galaxy.yml
- src: https://github.com/ItinerisLtd/trellis-wordfence-kinsta
  version: x.x.x # Check for latest version!
```

Run the command:
```bash
trellis galaxy install

# Alternatively
ansible-galaxy install -r galaxy.yml --force
```

## Role Variables

1. Add this role to the [`deploy_after` hook](https://roots.io/trellis/docs/deploys/#hooks):
    ```yaml
    # group_vars/all/deploy-hooks.yml
    # Learn more on https://roots.io/trellis/docs/deploys/#hooks
    deploy_after:
      - "{{ playbook_dir }}/vendor/roles/itinerisltd.trellis-wordfence-kinsta/tasks/main.yml"
    ```

## Usage

1. Setup the [role variables](#role-variables)
2. [Deploy](https://roots.io/trellis/docs/deploys/#example)
3. Tell Kinsta to add the `auto_prepend_file` variable that points to `{{ deploy_helper.current_path }}/web/wp/wordfence-waf.php`
    1. `deploy_helper.shared_path` can differ between Trellis setups. Check for final path before asking Kinsta.
    2. This is usually where the uploads are stored.
    3. E.g. `auto_prepend_file = '/www/kinstauser_123/public/current/web/wp/wordfence-waf.php'`

## FAQs

### WordFence still complains that the firewall is not configured!

Do not forget to tell Kinsta to add the `auto_prepend_file` variable.

## Testing

### Syntax Check

```bash
➜ ansible-playbook -i 'localhost,' --syntax-check tests/test.yml
```

## Author Information

[trellis-wordfence-kinsta](https://github.com/ItinerisLtd/trellis-wordfence-kinsta) is an [Itineris Limited](https://www.itineris.co.uk/) project created by [Lee Hanbury-Pickett](https://github.com/codepuncher).

Special thanks to [the Roots team](https://roots.io/about/) whose [Trellis](https://github.com/roots/trellis) make this project possible.

Full list of contributors can be found [here](https://github.com/ItinerisLtd/trellis-wordfence-kinsta/graphs/contributors).

## Feedback

**Please provide feedback!** We want to make this library useful in as many projects as possible.
Please submit an [issue](https://github.com/ItinerisLtd/trellis-wordfence-kinsta/issues/new) and point out what you do and don't like, or fork the project and make suggestions.
**No issue is too small.**

## Change log

Please see [CHANGELOG](./CHANGELOG.md) for more information on what has changed recently.

## License

[trellis-wordfence-kinsta](https://github.com/ItinerisLtd/trellis-wordfence-kinsta) is released under the [MIT License](https://opensource.org/licenses/MIT).
