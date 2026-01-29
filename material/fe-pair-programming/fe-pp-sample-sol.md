# Sample Solution

### Iteration 0: Project Setup

Goal: get the app running locally and understand the folder structure.

<details>
<summary>Solution (Iteration 0)</summary>

1) Clone the starter:

```bash
git clone https://github.com/tx00-resources-en/react-pp2 week3-fe-pair-programming
cd week3-fe-pair-programming
```

2) Remove the starter's Git history:

- Windows (PowerShell):

```powershell
Remove-Item -Recurse -Force .git
```

- macOS/Linux:

```bash
rm -rf .git
```

3) Install + run:

```bash
npm install
npm run dev
```

4) Sanity check: Font Awesome

Open `index.html` and verify this is in `<head>` (if it's already there, you're done):

```html
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.6.0/css/all.min.css"
/>
```

</details>

----

### Iteration 1: Navbar

Goal: replace the placeholder `Navbar` component with the real Navbar HTML converted to JSX.


<details>
<summary>Solution (Iteration 1)</summary>

Replace the placeholder code in `src/components/Navbar.jsx` with:

```jsx
import logo from '../assets/images/logo.svg'

const Navbar = () => {
  return (
    <nav className='navbar'>
      <div className='nav-center'>
        <div className='nav-header'>
          <img src={logo} className='nav-logo' alt='backroads' />
          <button type='button' className='nav-toggle' id='nav-toggle'>
            <i className='fas fa-bars'></i>
          </button>
        </div>
        <ul className='nav-links' id='nav-links'>
          <li>
            <a href='#home' className='nav-link'>
              home
            </a>
          </li>
          <li>
            <a href='#about' className='nav-link'>
              about
            </a>
          </li>
          <li>
            <a href='#services' className='nav-link'>
              services
            </a>
          </li>
          <li>
            <a href='#tours' className='nav-link'>
              tours
            </a>
          </li>
        </ul>
        <ul className='nav-icons'>
          <li>
            <a
              href='https://www.facebook.com'
              target='_blank'
              rel='noreferrer'
              className='nav-icon'
            >
              <i className='fab fa-facebook'></i>
            </a>
          </li>
          <li>
            <a
              href='https://www.x.com'
              target='_blank'
              rel='noreferrer'
              className='nav-icon'
            >
              <i className='fab fa-x-twitter'></i>
            </a>
          </li>
          <li>
            <a
              href='https://www.squarespace.com/'
              target='_blank'
              rel='noreferrer'
              className='nav-icon'
            >
              <i className='fab fa-squarespace'></i>
            </a>
          </li>
        </ul>
      </div>
    </nav>
  )
}

export default Navbar
```

</details>

----
### Iteration 2: Hero, About, Services, Tours, Footer

Goal: convert the rest of the HTML sections into React components.

<details>
<summary>Solution (Iteration 2)</summary>

These are working reference solutions you can paste into each component.

`src/components/Hero.jsx`

```jsx
const Hero = () => {
  return (
    <section className='hero' id='home'>
      <div className='hero-banner'>
        <h1>backroads app</h1>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Vitae
          explicabo debitis est autem dicta.
        </p>
        <a href='#tours' className='btn hero-btn'>
          explore tours
        </a>
      </div>
    </section>
  )
}

export default Hero
```

`src/components/About.jsx`

```jsx
import aboutImg from '../assets/images/about.jpeg'

const About = () => {
  return (
    <section className='section' id='about'>
      <div className='section-title'>
        <h2>
          about <span>us</span>
        </h2>
      </div>
      <div className='section-center about-center'>
        <div className='about-img'>
          <img src={aboutImg} className='about-photo' alt='awesome beach' />
        </div>
        <article className='about-info'>
          <h3>explore the difference</h3>
          <p>
            Lorem ipsum, dolor sit amet consectetur adipisicing elit.
            Aspernatur quisquam harum nam cumque temporibus explicabo dolorum
            sapiente odio unde dolor?
          </p>
          <p>
            Lorem ipsum, dolor sit amet consectetur adipisicing elit.
            Aspernatur quisquam harum nam cumque temporibus explicabo dolorum
            sapiente odio unde dolor?
          </p>
          <a href='#' className='btn'>
            read more
          </a>
        </article>
      </div>
    </section>
  )
}

export default About
```

`src/components/Services.jsx`

```jsx
const Services = () => {
  return (
    <section className='section services' id='services'>
      <div className='section-title'>
        <h2>
          our <span>services</span>
        </h2>
      </div>
      <div className='section-center services-center'>
        <article className='service'>
          <span className='service-icon'>
            <i className='fas fa-wallet fa-fw'></i>
          </span>
          <div className='service-info'>
            <h4 className='service-title'>saving money</h4>
            <p className='service-text'>
              Lorem ipsum dolor sit amet consectetur adipisicing elit
              Asperiores, officia.
            </p>
          </div>
        </article>

        <article className='service'>
          <span className='service-icon'>
            <i className='fas fa-tree fa-fw'></i>
          </span>
          <div className='service-info'>
            <h4 className='service-title'>endless hiking</h4>
            <p className='service-text'>
              Lorem ipsum dolor sit amet consectetur adipisicing elit
              Asperiores, officia.
            </p>
          </div>
        </article>

        <article className='service'>
          <span className='service-icon'>
            <i className='fas fa-socks fa-fw'></i>
          </span>
          <div className='service-info'>
            <h4 className='service-title'>amazing comfort</h4>
            <p className='service-text'>
              Lorem ipsum dolor sit amet consectetur adipisicing elit
              Asperiores, officia.
            </p>
          </div>
        </article>
      </div>
    </section>
  )
}

export default Services
```

`src/components/Tours.jsx`

```jsx
import tour1 from '../assets/images/tour-1.jpeg'
import tour2 from '../assets/images/tour-2.jpeg'
import tour3 from '../assets/images/tour-3.jpeg'
import tour4 from '../assets/images/tour-4.jpeg'

const Tours = () => {
  return (
    <section className='section' id='tours'>
      <div className='section-title'>
        <h2>
          featured <span>tours</span>
        </h2>
      </div>
      <div className='section-center featured-center'>
        <article className='tour-card'>
          <div className='tour-img-container'>
            <img src={tour1} className='tour-img' alt='Tibet Adventure' />
            <p className='tour-date'>august 26th, 2027</p>
          </div>
          <div className='tour-info'>
            <div className='tour-title'>
              <h4>Tibet Adventure</h4>
            </div>
            <p>
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cumque
              vitae tempore voluptatum maxime reprehenderit eum quod
              exercitationem fugit, qui corporis.
            </p>
            <div className='tour-footer'>
              <p>
                <span>
                  <i className='fas fa-map'></i>
                </span>
                china
              </p>
              <p>from €2100</p>
              <p>6 days</p>
            </div>
          </div>
        </article>

        <article className='tour-card'>
          <div className='tour-img-container'>
            <img src={tour2} className='tour-img' alt='best of java' />
            <p className='tour-date'>october 1th, 2027</p>
          </div>
          <div className='tour-info'>
            <div className='tour-title'>
              <h4>best of java</h4>
            </div>
            <p>
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cumque
              vitae tempore voluptatum maxime reprehenderit eum quod
              exercitationem fugit, qui corporis.
            </p>
            <div className='tour-footer'>
              <p>
                <span>
                  <i className='fas fa-map'></i>
                </span>
                indonesia
              </p>
              <p>from €1400</p>
              <p>11 days</p>
            </div>
          </div>
        </article>

        <article className='tour-card'>
          <div className='tour-img-container'>
            <img src={tour3} className='tour-img' alt='explore hong kong' />
            <p className='tour-date'>september 15th, 2027</p>
          </div>
          <div className='tour-info'>
            <div className='tour-title'>
              <h4>explore hong kong</h4>
            </div>
            <p>
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cumque
              vitae tempore voluptatum maxime reprehenderit eum quod
              exercitationem fugit, qui corporis.
            </p>
            <div className='tour-footer'>
              <p>
                <span>
                  <i className='fas fa-map'></i>
                </span>
                hong kong
              </p>
              <p>from €5000</p>
              <p>8 days</p>
            </div>
          </div>
        </article>

        <article className='tour-card'>
          <div className='tour-img-container'>
            <img src={tour4} className='tour-img' alt='kenya highlights' />
            <p className='tour-date'>december 5th, 2027</p>
          </div>
          <div className='tour-info'>
            <div className='tour-title'>
              <h4>kenya highlights</h4>
            </div>
            <p>
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cumque
              vitae tempore voluptatum maxime reprehenderit eum quod
              exercitationem fugit, qui corporis.
            </p>
            <div className='tour-footer'>
              <p>
                <span>
                  <i className='fas fa-map'></i>
                </span>
                kenya
              </p>
              <p>from €3300</p>
              <p>20 days</p>
            </div>
          </div>
        </article>
      </div>
    </section>
  )
}

export default Tours
```

`src/components/Footer.jsx`

```jsx
const Footer = () => {
  const year = new Date().getFullYear()

  return (
    <footer className='section footer'>
      <ul className='footer-links' id='nav-links'>
        <li>
          <a href='#home' className='footer-link'>
            home
          </a>
        </li>
        <li>
          <a href='#about' className='footer-link'>
            about
          </a>
        </li>
        <li>
          <a href='#services' className='footer-link'>
            services
          </a>
        </li>
        <li>
          <a href='#tours' className='footer-link'>
            tours
          </a>
        </li>
      </ul>
      <ul className='footer-icons'>
        <li>
          <a
            href='https://www.facebook.com'
            target='_blank'
            rel='noreferrer'
            className='footer-icon'
          >
            <i className='fab fa-facebook'></i>
          </a>
        </li>
        <li>
          <a
            href='https://www.twitter.com'
            target='_blank'
            rel='noreferrer'
            className='footer-icon'
          >
            <i className='fab fa-twitter'></i>
          </a>
        </li>
        <li>
          <a
            href='https://www.squarespace.com/'
            target='_blank'
            rel='noreferrer'
            className='footer-icon'
          >
            <i className='fab fa-squarespace'></i>
          </a>
        </li>
      </ul>
      <p className='copyright'>
        copyright © travel tours company {year}. all rights reserved
      </p>
    </footer>
  )
}

export default Footer
```

</details>


### Iteration 3: Title + Services refactor (data-driven)

Goal: practice props + mapping by rendering services from `src/data.js`.


<details>
<summary>Solution (Iteration 3)</summary>

`src/components/Title.jsx`

```jsx
const Title = ({ title, subTitle }) => {
  return (
    <div className='section-title'>
      <h2>
        {title} <span>{subTitle}</span>
      </h2>
    </div>
  )
}

export default Title
```

`src/components/Service.jsx`

```jsx
const Service = ({ icon, title, text }) => {
  return (
    <article className='service'>
      <span className='service-icon'>
        <i className={icon}></i>
      </span>
      <div className='service-info'>
        <h4 className='service-title'>{title}</h4>
        <p className='service-text'>{text}</p>
      </div>
    </article>
  )
}

export default Service
```

`src/components/Services.jsx`

```jsx
import { services } from '../data'
import Title from './Title'
import Service from './Service'

const Services = () => {
  return (
    <section className='section services' id='services'>
      <Title title='our' subTitle='services' />

      <div className='section-center services-center'>
        {services.map((service) => {
          return <Service {...service} key={service.id} />
        })}
      </div>
    </section>
  )
}

export default Services
```

</details>

DevTools check:

![](./fe-pair-programming/img/services.png)

----
### Iteration 4: 

Goal: practice mapping + reusable components by rendering tours from `src/data.js`.


<details>
<summary>Solution (Iteration 4)</summary>

`src/components/Tour.jsx`

```jsx
const Tour = ({ image, date, title, info, location, duration, cost }) => {
  return (
    <article className='tour-card'>
      <div className='tour-img-container'>
        <img src={image} className='tour-img' alt={title} />
        <p className='tour-date'>{date}</p>
      </div>
      <div className='tour-info'>
        <div className='tour-title'>
          <h4>{title}</h4>
        </div>
        <p>{info}</p>
        <div className='tour-footer'>
          <p>
            <span>
              <i className='fas fa-map'></i>
            </span>
            {location}
          </p>
          <p>from €{cost}</p>
          <p>{duration} days</p>
        </div>
      </div>
    </article>
  )
}

export default Tour
```

`src/components/Tours.jsx`

```jsx
import { tours } from '../data'
import Title from './Title'
import Tour from './Tour'

const Tours = () => {
  return (
    <section className='section' id='tours'>
      <Title title='featured' subTitle='tours' />
      <div className='section-center featured-center'>
        {tours.map((tour) => {
          return <Tour key={tour.id} {...tour} />
        })}
      </div>
    </section>
  )
}

export default Tours
```

</details>

- You can use the React DevTools extension to inspect the component hierarchy. When you do, you should see the following structure:
![](./fe-pair-programming/img/tours.png)

----
### Iteration 5: 

Goal: create reusable nav links from data (so you don't copy/paste `<li><a ...>` everywhere).


<details>
<summary>Solution (Iteration 5)</summary>

`src/components/PageLink.jsx`

```jsx
const PageLink = ({ link, itemClass }) => {
  return (
    <li>
      <a href={link.href} className={itemClass}>
        {link.text}
      </a>
    </li>
  )
}

export default PageLink
```

`src/components/PageLinks.jsx`

```jsx
import { pageLinks } from '../data'
import PageLink from './PageLink'

const PageLinks = ({ parentClass, itemClass }) => {
  return (
    <ul className={parentClass} id='nav-links'>
      {pageLinks.map((link) => {
        return <PageLink key={link.id} link={link} itemClass={itemClass} />
      })}
    </ul>
  )
}

export default PageLinks
```

In `src/components/Footer.jsx`, replace the static `<ul className='footer-links' ...>` with:

```jsx
<PageLinks parentClass='footer-links' itemClass='footer-link' />
```

</details>

----
### Iteration 6: 

Goal: refactor the navbar to reuse `PageLinks`, and refactor social icons to reuse `SocialLink`.

- You can use the React DevTools extension to inspect the component hierarchy. When you do, you should see the following structure:
![](./fe-pair-programming/img/navbar.png)

<details>
<summary>Solution (Iteration 6)</summary>

`src/components/SocialLink.jsx`

```jsx
const SocialLink = ({ link, itemClass }) => {
  return (
    <li>
      <a
        href={link.href}
        target='_blank'
        rel='noreferrer'
        className={itemClass}
      >
        <i className={link.icon}></i>
      </a>
    </li>
  )
}

export default SocialLink
```

`src/components/SocialLinks.jsx`

```jsx
import { socialLinks } from '../data'
import SocialLink from './SocialLink'

const SocialLinks = ({ parentClass, itemClass }) => {
  return (
    <ul className={parentClass}>
      {socialLinks.map((link) => {
        return <SocialLink key={link.id} link={link} itemClass={itemClass} />
      })}
    </ul>
  )
}

export default SocialLinks
```

`src/components/Navbar.jsx` (refactor to use `PageLinks` + `SocialLinks`)

```jsx
import logo from '../assets/images/logo.svg'
import PageLinks from './PageLinks'
import SocialLinks from './SocialLinks'

const Navbar = () => {
  return (
    <nav className='navbar'>
      <div className='nav-center'>
        <div className='nav-header'>
          <img src={logo} className='nav-logo' alt='backroads' />
          <button type='button' className='nav-toggle' id='nav-toggle'>
            <i className='fas fa-bars'></i>
          </button>
        </div>

        <PageLinks parentClass='nav-links' itemClass='nav-link' />
        <SocialLinks parentClass='nav-icons' itemClass='nav-icon' />
      </div>
    </nav>
  )
}

export default Navbar
```

</details>

----
### Iteration 7

Currently, the `Navbar` component contains the `Header` component inside it:

```jsx
function Navbar() {
  return (
    <nav className="navbar">
      <div className="nav-center">
        <Header />
        <PageLinks parentClass="nav-links" itemClass="nav-link" />
        <SocialLinks parentClass="nav-icons" itemClass="nav-icon" />
      </div>
    </nav>
  );
}

export default Navbar;
```

Goal: improve semantics by making the `Header` component wrap the `Navbar`.

<details>
<summary>Solution (Iteration 7)</summary>

`src/App.jsx` (render `Header` instead of `Navbar`)

```jsx
import About from './components/About'
import Footer from './components/Footer'
import Header from './components/Header'
import Hero from './components/Hero'
import Services from './components/Services'
import Tours from './components/Tours'
import './App.css'

function App() {
  return (
    <div>
      <Header />
      <Hero />
      <About />
      <Services />
      <Tours />
      <Footer />
    </div>
  )
}

export default App
```

`src/components/Header.jsx` (wrap the navbar)

```jsx
import Navbar from './Navbar'

const Header = () => {
  return (
    <header>
      <Navbar />
    </header>
  )
}

export default Header
```

Optional (CSS): If you want to style the header later, you can add a class.

1) Update the header tag:

```jsx
// OPTIONAL
<header className='site-header'>
  <Navbar />
</header>
```

2) Add CSS (optional) in `src/App.css`:

```css
/* OPTIONAL */
.site-header {
  /* Example: keep it above the page content */
  position: relative;
  z-index: 2;
}
```

`src/components/Navbar.jsx` (make sure it does NOT render `Header` anymore)

Keep Navbar responsible only for the `<nav>` and its contents (logo, links, icons).

</details>


