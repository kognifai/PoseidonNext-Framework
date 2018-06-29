# Description
The Poseidon dropdown directive toggles the visibility of a dropdown menu. It's used with Design System Dropdown component ( ```kx-dropdown```). The menu is shown when the toggle element is clicked/tapped and hidden when clicking/tapping outside.
# Usage
The directive is applied by adding 'appDropdown' attribute to ```kx-dropdown__toggle``` inside ```kx-dropdown```.
```html
<div class="kx-dropdown" role="group">
  <button id="--34709" class="kx-dropdown__toggle kx-btn kx-btn--size-base kx-btn--icon kx-js-dropdown__toggle"
  aria-haspopup="true" aria-expanded="false" appDropdown>
    <span class="kx-btn__inner">
      <i class="kx-icon kx-icon--size-base">
        <svg focusable="false">
          <use xlink:href="./node_modules/kognifai-design-system/www/assets/img/icons/sprites/icons.svg#user"/>
        </svg>
      </i>
      <span class="kx-btn__txt kx-is-vishidden">User</span>
    </span>
  </button>
  <div class="kx-dropdown__menu kx-dropdown__menu--align-right kx-js-dropdown__menu" aria-labelledby="--34709">
    <ul class="kx-dropdown__list">
      <li class="kx-dropdown__item">
        <a class="kx-dropdown__link header-dropdown-link" href="#">
          <span class="kx-dropdown__item__txt">User profile</span>
        </a>
      </li>
      <li class="kx-divider kx-divider--size-mini" aria-hidden="true" tabindex="-1"/>
      <li class="kx-dropdown__item">
        <a class="kx-dropdown__link header-dropdown-link" href="#">
          <span class="kx-dropdown__item__txt">Logout</span>
        </a>
      </li>
    </ul>
  </div>
</div>
```