![Languages](https://img.shields.io/github/languages/top/Sweesz/Abramoil--oil-trade-website)
![License](https://img.shields.io/badge/License-Educational-blue)
# Abramoil — Educational Project

## About the Project

**Abramoil** is an educational project — a multi-page website for a fictional international company specializing in the wholesale trade of petroleum products.

**Main goal of the project:** build a beautiful, modern, and responsive website on the theme of oil using **only HTML and CSS** — no JavaScript, no third-party frameworks.

Additionally, a lightweight server-side part was implemented in **Rust** using the **Axum** web framework, which serves the static files of the site.

---

## Goals and Objectives

- Create a multi-page website (home, about, products, trade, contacts).
- Design an attractive "oil-themed" visual style.
- Use **only HTML and CSS** — no JS, no CSS frameworks (Bootstrap, Tailwind, etc.).
- Ensure responsiveness across devices.
- Implement navigation between pages.
- (Bonus) Write a simple static-file server in **Rust** with **Axum**.

---

## Technologies

### Frontend
| Technology | Purpose |
|------------|---------|
| **HTML5** | Semantic page markup |
| **CSS3** | Styling, animations, responsiveness |
| **Google Fonts** | Montserrat and Open Sans typefaces |

> ❗ JavaScript is **not used** — all interactivity and styling are implemented purely with CSS.

### Backend
| Technology | Purpose |
|------------|---------|
| **Rust** | Systems programming language used for the server |
| **Axum** | Web framework for routing and serving files |
| **Tokio** | Asynchronous runtime for Rust |
| **tower-http** (`ServeDir`) | Middleware for serving static files from a directory |

The server simply serves the static site from the `sites/` directory on `http://127.0.0.1:3000`.

---

## Project Structure

```
abramoil/
├── sites/                  # Static site files served by the Rust backend
│   ├── index.html          # Home page
│   ├── about.html          # About the Company
│   ├── product.html        # Products
│   ├── commerce.html       # Trade
│   ├── contacts.html       # Contacts
│   ├── styles/
│   │   └── style.css       # Main stylesheet
│   ├── img/                # Images and posters
│   └── mainvid.mp4         # Background video on the home page
├── src/
│   └── main.rs             # Rust + Axum server
├── Cargo.lock
├── Cargo.toml              # Rust dependencies
├── .gitignore
└── README.md
```

---

## Site Pages

| Page | Description |
|------|-------------|
| **index.html** | Home page with background video, tagline, and a "Contact Us" button |
| **about.html** | Company information |
| **product.html** | Catalog of petroleum products (AI-95, diesel, fuel oil, LPG) |
| **commerce.html** | Global trade and company statistics |
| **contacts.html** | Contact details and offices |

---

## Design Highlights

- Background video on the home page (HTML5 `<video>` with `autoplay`, `muted`, `loop`).
- Themed backgrounds per page (`bg-about`, `bg-trading`, `bg-contacts`, `bg-products`).
- Product and statistics cards.
- Unified header with logo and navigation.
- Responsive layout via CSS.

---

## Running the Project

### Requirements
- [Rust toolchain](https://rustup.rs/) (stable)
- `cargo` package manager

### Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/abramoil.git
   cd abramoil
   ```

2. Build and run the server:
   ```bash
   cargo run
   ```

3. Open your browser at:
   ```
   http://127.0.0.1:3000
   ```

The Axum server serves the contents of the `sites/` directory as static files, so `index.html` becomes the home page at `/`.

### How the server works

```rust
use axum::{Router};
use std::net::SocketAddr;
use tower_http::services::ServeDir;

#[tokio::main]
async fn main() {
    let app = Router::new()
        .nest_service("/", ServeDir::new("sites"));

    let addr = SocketAddr::from(([127, 0, 0, 1], 3000));
    println!("Server running on http://{}", addr);

    axum::serve(
        tokio::net::TcpListener::bind(addr).await.unwrap(),
        app,
    ).await.unwrap();
}
```

- `ServeDir::new("sites")` — serves all files from the `sites/` folder.
- `nest_service("/", ...)` — mounts the static-file service at the root path.
- The server listens on `127.0.0.1:3000`.

---

## A Note on the Name

The name **Abramoil** is a playful nod to **Roman Arkadyevich Abramovich** — a well-known Russian businessman and billionaire, best known internationally as the former owner of **Chelsea Football Club** (London) and as one of the most prominent figures in the Russian oil industry. He built his fortune in the 1990s through the oil sector, most notably via the Sibneft oil company, and later became a major shareholder in Evraz (steel) and other industrial assets.

Because of his strong association with the oil business in the 1990s — the same era referenced on the site's homepage ("Global petroleum products trading since the '90s") — the fictional company was named **Abramoil** as a light-hearted tribute. The name is a wordplay combining "Abramovich" and "oil."

> ⚠️ Abramoil is a **fictional** company. It is not affiliated with Roman Abramovich or any real organization.

---

## Author

**Yaroslav Nikitich Vorontsov** — developer and owner of the project.


---

## Disclaimer

**Abramoil** is a fictional company created solely for educational purposes. Any resemblance to real organizations is purely coincidental. The project is inspired by the name of Roman Arkadyevich Abramovich (Abramovich oil).

---

## License

This project was created for educational purposes and is not intended for commercial use.
