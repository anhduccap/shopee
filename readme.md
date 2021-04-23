# PROJECT SHOPEE
Demo Shopee UI with knowledge gained from [F8 Frontend Course](https://fullstack.edu.vn/courses)

## Create Source Code Base
### Folder tree
- index.html
- assets
    - styles
        - base.css 
            `font-size: 62.5%` mean: 1rem = 10px -> ease to use
            `grid` is also part of base.css
        - main.css
    - images
    - fonts
### Reset CSS
#### Reason:
- Some HTML tags (body, h1, h2, ...) have unwanted margin and padding properties.
- Different browsers will have different values.
--> We must reset them
#### Doing (2 ways)
- Write code into main.css file (padding: 0; margin: 0; ...).
- Use [Normalize](https://cdnjs.com/libraries/normalize)
!!! When we add link into HTML header, remember that library or reuseable file should be add first, main.css is next. Main.css file will have highest priority if we need to edit them later.
## Detail Design
Always have `app` class contains all website's components
### Header
#### 1. Navbar
- All `li` tag will have an `a` tag inside to link to other pages.
- CSS 2 `ul` tag with `display: flex;` + `justify-content: space-between;`
- `ul` have default padding left -> have distance with left side -> `padding: 0;`
- Create `grid` tag which cover all navbar. We don't create like that: `<header class="header grid">` because header background must cover all width, only header's content apply `width: 1200px`
- Right border of item don't have on all item -> create modifier `header__nav-item-link--right-border`
- Create QR Code hover: `Tải ứng dunjg` will have `position: relative` and QR code will have `position: absolute`
- In QR notification component, when we add images (logo app store, google play,...) without `a tag` cover outside, the image will be distorted (méo mó)
- When we hover on `li`tag, QR code will be appear, but we can't hover on QR code because `.header__nav-item--show-qr:hover .header__qr` class active when hover on `li` -> We can add a pseudo element (::after)
#### 2. Modal login/register
- When we click on "Đăng nhập" or "Đăng ký" button, the modal form will be shown: modal__overlay is a rgba color layer with opacity < 1 -> show below components 
- Default z-index of an element equal to 0 -> body is above the overlay because it's add later
- We wanna body always above -> set z-index = 1
#### 3. Search
- For elements that appear when be interacted (hover to show notifications, QR code, search history,...), we have to put them and their parent in the same block, and set their position is absolute (compare to their parent)
- When we work with radius-border attribute, notice that pseudo class hover can make design incorrectly. For example with search history, the last element border have no border-radius attribute -> bottom-left and bottom-right angle will be shown incorrectly (using pseudo class last-child)
!!! UX bug: When we hover on after or before pseudo class, `cursor: pointer` will be disappeared. The cause is after or before pseudo class. It has no cursor attribute.