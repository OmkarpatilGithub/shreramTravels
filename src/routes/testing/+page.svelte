<script>
  let menuOpen = false;
  let quickType = "With driver";
  let quickPickup = "Pune, Maharashtra";
  let quickDrop = "";

  let quoteName = "";
  let quotePhone = "";
  let quoteType = "Car with driver";
  let quoteCar = "Hatchback";
  let quoteDate = "";
  let quoteReturnDate = "";
  let quoteRoute = "";
  let submitted = false;
  const today = new Date().toISOString().split("T")[0];

  function handleQuickSubmit(e) {
    e.preventDefault();
    quoteType = quickType;
    quoteRoute = `${quickPickup}${quickDrop ? " - " + quickDrop : ""}`;
    document.getElementById("quote")?.scrollIntoView({ behavior: "smooth" });
  }

  function handleQuoteSubmit(e) {
    e.preventDefault();
    submitted = true;
  }

  let activeFilter = "all";
  const tabs = [
    { label: "All cars", value: "all" },
    { label: "With driver", value: "driver" },
    { label: "Group travel", value: "group" }
  ];

  const cars = [
    {
      types: ["driver"],
      badge: "Budget friendly",
      emoji: "🚙",
      title: "Hatchback",
      desc: "Swift, i20 or similar. Best for city use and short trips.",
      meta: ["4 seats", "AC", "Local use"],
      priceLabel: "from",
      price: "₹1,899/day"
    },
    {
      types: ["driver"],
      badge: "Most popular",
      emoji: "🚘",
      title: "Sedan",
      desc: "Dzire, Aura or similar. Comfortable for Pune-Mumbai and business trips.",
      meta: ["4 seats", "Large boot", "Driver option"],
      priceLabel: "from",
      price: "₹12/km"
    },
    {
      types: ["driver", "group"],
      badge: "Family choice",
      emoji: "🚐",
      title: "SUV / MUV",
      desc: "Ertiga, Innova or similar. Ideal for family trips, luggage and long highway drives.",
      meta: ["6-7 seats", "AC", "Outstation"],
      priceLabel: "from",
      price: "₹17/km"
    },
    {
      types: ["group"],
      badge: "Group travel",
      emoji: "🚌",
      title: "Tempo Traveller",
      desc: "12 to 17 seater vehicles for office outings, weddings, pilgrimage and group tours.",
      meta: ["12-17 seats", "Driver", "Luggage space"],
      priceLabel: "from",
      price: "₹24/km"
    },
    {
      types: ["driver"],
      badge: "Premium",
      emoji: "🏎️",
      title: "Luxury cars",
      desc: "Premium sedans and SUVs for weddings, VIP movement, corporate guests and special days.",
      meta: ["Premium", "On request", "Driver option"],
      priceLabel: "custom",
      price: "Get quote"
    },
    {
      types: ["driver"],
      badge: "Airport ready",
      emoji: "🚕",
      title: "Airport cab",
      desc: "Dedicated pickup and drop service for Pune Airport, Mumbai Airport and railway stations.",
      meta: ["On time", "AC", "Local support"],
      priceLabel: "from",
      price: "₹999"
    }
  ];

  $: visibleCars = cars.filter((c) => activeFilter === "all" || c.types.includes(activeFilter));

  const aboutPoints = [
    { n: "01", title: "Right vehicle for the route", text: "Compact cars for city use, sedans for business travel, SUVs for family trips, and tempo travellers for groups." },
    { n: "02", title: "Rental terms explained upfront", text: "Fare, kilometre limits, tolls, parking, fuel policy, deposit and driver allowance are discussed before confirmation." },
    { n: "03", title: "Direct Pune contact", text: "Customers can call or WhatsApp directly instead of dealing with a faceless marketplace or delayed callback system." }
  ];

  const services = [
    { icon: "👨‍✈️", title: "Car with driver", text: "Verified drivers for local sightseeing, meetings, events, family functions and outstation routes." },
    { icon: "✈️", title: "Airport transfer", text: "Pune Airport, Mumbai Airport and railway-station pickups with clean vehicles and punctual reporting." },
    { icon: "📅", title: "Monthly rentals", text: "Company staff transport, executive cars and long-term vehicle needs with custom monthly pricing." },
    { icon: "🧳", title: "Outstation trips", text: "One-way, round-trip and multi-city travel plans across Maharashtra and India." }
  ];

  const checklist = [
    { n: 1, title: "Share dates and car type", text: "Tell us your pickup date, return date, route and preferred vehicle category." },
    { n: 2, title: "Get a clear rental plan", text: "We confirm fare, kilometre limit, fuel policy, pickup point and support contact before booking." },
    { n: 3, title: "Drive with support", text: "Our Pune desk stays reachable for route help, extension requests and roadside coordination." },
    { n: 4, title: "Start your rental", text: "Receive car details, support number and final checklist before pickup or driver reporting." }
  ];

  const puneRoutes = ["Pune → Mumbai", "Pune → Nashik", "Pune → Goa", "Pune → Mahabaleshwar", "Pune → Shirdi", "Pune → Lonavala"];

  const cities = [
    { name: "Pune", image: "/pune.png" },
    { name: "Mumbai", image: "/mumbai.png" },
    { name: "Goa", image: "/goa.png" },
    { name: "Nashik", image: "/nashik.png" },
    { name: "Shirdi", image: "/shirdi.png" },
    { name: "Lonavala", image: "/lonavala.png" }
  ];

  const steps = [
    { n: 1, title: "Send trip details", text: "Share rental type, pickup city, destination or usage, dates, car category and driver preference." },
    { n: 2, title: "Get vehicle options", text: "We confirm available cars, seating, luggage suitability, estimated fare and pickup reporting time." },
    { n: 3, title: "Confirm documents", text: "For driver rentals, we confirm route, tolls, parking and allowance terms." },
    { n: 4, title: "Start your rental", text: "Receive car details, support number and final checklist before pickup or driver reporting." }
  ];

  const fareList = [
    "Vehicle category and rental duration",
    "Per-km or per-day rate, depending on service",
    "Driver allowance for outstation rentals when applicable",
    "Toll, parking, state tax and permit handling explained upfront",
    "Fuel policy and extra-km charges explained before confirmation"
  ];

  const whyItems = [
    { icon: "✓", title: "Vehicle options for every use", text: "Driver cars, airport cabs, SUVs, tempo travellers and premium cars from one provider." },
    { icon: "₹", title: "Transparent quotes", text: "We explain per-km charges, day limits, toll/parking, driver allowance and deposit terms clearly." },
    { icon: "☎", title: "Direct owner-style contact", text: "Call or WhatsApp the Pune team directly instead of waiting for a generic marketplace response." }
  ];

  const reviews = [
    { text: 'Booked a Pune to Mumbai cab at short notice. Clean car, clear fare and the driver reported on time.', initials: "AG", name: "Amit G.", tag: "Outstation rental" },
    { text: 'We used a Tempo Traveller for a family trip from Pune to Goa. Good vehicle condition and helpful support throughout.', initials: "PR", name: "Priya R.", tag: "Family Trip" },
    { text: 'We used an SUV for a family trip from Pune. Good vehicle condition and helpful support throughout.', initials: "SK", name: "Sachin K.", tag: "Family Trip" }
  ];

  const faqs = [
    { q: "Can I book a car with driver for outstation trips?", a: "Yes. We provide chauffeur-driven cars for Pune local, one-way, round-trip and multi-city outstation rentals across India." },
    { q: "Are tolls and parking included?", a: "It depends on the route and rental plan. We explain tolls, parking, state tax, permit and driver allowance before confirmation." },
    { q: "How fast can I confirm a booking?", a: "For urgent bookings, call or WhatsApp 72182 83271. Availability depends on date, route, vehicle category and rental type." },
    { q: "Do you offer monthly or corporate rentals?", a: "Yes. Monthly rentals, executive cars and company transport can be quoted based on vehicle type, daily usage and reporting location." },
    { q: "Which areas do you serve?", a: "We are based in Pune, Maharashtra and support local, airport, Maharashtra outstation and all-India rental requirements." }
  ];

  const waLink = "https://wa.me/91914663456?text=Hello%20Shree%20Ram%20Travels%2C%20I%20need%20a%20car%20rental%20quote.";
</script>

<svelte:head>
  <title>Shree Ram Travels | Pune Car Rentals</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
</svelte:head>

<main>
  <div class="topbar">
    <div class="container topbar-inner">
      <span class="dot"></span>
      <span>Pune, Maharashtra based</span>
      <span>Cars across India</span>
      <span>Call: +91 72182 83271 / +91 914663456</span>
    </div>
  </div>

  <header class="header">
    <nav class="container nav">
      <a href="#" class="brand"><span class="brand-mark">S</span><span>Shree Ram Travels</span></a>

      <div class:open={menuOpen} class="nav-links">
        <a href="#about">About</a>
        <a href="#services">Services</a>
        <a href="#fleet">Fleet</a>
        <a href="#process">Process</a>
        <a href="#routes">Routes</a>
        <a href="#faq">FAQ</a>
        <a href="#why">Why us</a>
      </div>

      <div class="nav-actions desktop-only">
        <a href="tel:+917218283271" class="btn ghost">Call now</a>
        <a href="#quote" class="btn primary">Book a car</a>
      </div>

      <button class="menu-btn" aria-label="Open menu" on:click={() => (menuOpen = !menuOpen)}>☰</button>
    </nav>
  </header>

  <section class="hero">
    <div class="container hero-inner">
      <div class="hero-copy">
        <div class="eyebrow">Car rentals from Pune across India</div>
        <h1>Pune car rentals, <em>done clearly.</em></h1>
        <p>Book chauffeur-driven vehicles from Shree Ram Travels for Pune local travel, airport transfers, outstation routes, one-way drops and monthly business use across India.</p>
        <div class="actions">
          <a href="#quote" class="btn primary">Get instant quote</a>
          <a href={waLink} target="_blank" rel="noopener" class="btn ghost light">WhatsApp us</a>
        </div>
        <div class="trust">
          <span>Trusted by Pune families, renters and businesses</span>
          <span>Clean cars</span>
          <span>Transparent fares</span>
          <span>24/7 road support</span>
        </div>
      </div>

      <form class="quick-card" on:submit|preventDefault={handleQuickSubmit}>
        <label>Rental type
          <select bind:value={quickType}>
            <option>With driver</option>
            <option>Airport transfer</option>
            <option>Monthly rental</option>
          </select>
        </label>
        <label>Pickup city
          <input bind:value={quickPickup} />
        </label>
        <label>Destination / usage
          <input bind:value={quickDrop} placeholder="Mumbai, Goa, local Pune, etc." />
        </label>
        <button type="submit" class="btn primary wide">Check availability</button>
      </form>
    </div>
  </section>

  <section class="container metrics">
    <div class="metric"><b>24/7</b><span>booking and trip support</span></div>
    <div class="metric"><b>All India</b><span>outstation service routes</span></div>
    <div class="metric"><b>Pune</b><span>pickup and local expertise</span></div>
    <div class="metric"><b>Driver only</b><span>Self-drive removed</span></div>
  </section>

  <section id="about" class="section container">
    <div class="grid about-grid">
      <div class="card about-card">
        <div class="eyebrow accent">About Shree Ram Travels</div>
        <h2 class="section-title">Pune-based car rental service with an all-India mindset.</h2>
        <p class="muted">Shree Ram Travels is built for people who need a dependable vehicle without confusion: families planning outstation travel, professionals moving between cities, visitors landing at Pune or Mumbai airport.</p>
        <p class="muted">Our work is simple: understand the route, suggest the right car, explain the fare clearly, and stay reachable during the rental. Whether it is Pune local use, a Maharashtra weekend route, a one-way airport drop, or a longer all-India journey, the booking starts with direct human support.</p>
        <div class="pills">
          <span class="pill">Pune local rentals</span>
          <span class="pill">Outstation cabs</span>
          <span class="pill">Corporate monthly cars</span>
        </div>
      </div>
      <div class="card promise-list">
        {#each aboutPoints as point}
          <div class="promise-item">
            <div class="promise-num">{point.n}</div>
            <div>
              <h3>{point.title}</h3>
              <p class="muted">{point.text}</p>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <section id="services" class="section container">
    <div class="section-head">
      <div class="eyebrow accent">What we offer</div>
      <h2 class="section-title">Car rental services built for real Indian roads.</h2>
      <p class="muted">Focused only on rentals: no package clutter. Pick the service you need, get a clear fare, and travel with support from our Pune team.</p>
    </div>
    <div class="grid services-grid">
      {#each services as s}
        <article class="card service-card">
          <div class="service-icon">{s.icon}</div>
          <h3>{s.title}</h3>
          <p class="muted">{s.text}</p>
        </article>
      {/each}
    </div>
  </section>

  <section id="fleet" class="section section-alt">
    <div class="container">
      <div class="section-head">
        <div class="eyebrow accent">Choose your car</div>
        <h2 class="section-title">Fleet options for driver rentals.</h2>
        <p class="muted">Rates shown are sample starting prices for presentation. Final fare depends on car availability, route, dates, fuel plan and rental duration.</p>
      </div>

      <div class="tabs">
        {#each tabs as tab}
          <button class:active={activeFilter === tab.value} class="tab" on:click={() => (activeFilter = tab.value)}>{tab.label}</button>
        {/each}
      </div>

      <div class="grid cars-grid">
        {#each visibleCars as car}
          <article class="card car-card">
            <div class="car-hero">
              <span class="car-badge">{car.badge}</span>
              <div class="car-emoji">{car.emoji}</div>
            </div>
            <div class="card-body">
              <h3 class="car-title">{car.title}</h3>
              <p class="muted">{car.desc}</p>
              <div class="meta">
                {#each car.meta as m}
                  <span class="meta-item">{m}</span>
                {/each}
              </div>
              <div class="card-footer">
                <div>
                  <small class="muted">{car.priceLabel}</small>
                  <strong class="price">{car.price}</strong>
                </div>
                <a href="#quote" class="link">Book →</a>
              </div>
            </div>
          </article>
        {/each}
      </div>
    </div>
  </section>

  <section id="quote" class="section section-dark">
    <div class="container">
      <div class="section-head light-head">
        <div class="eyebrow accent-light">Quick quote</div>
        <h2 class="section-title">Private, flexible and ready when you are.</h2>
        <p class="muted light">Cars are available from Pune for verified customers. Submit your route and dates so our team can confirm vehicle availability and the best fare.</p>
      </div>

      <div class="grid quote-grid">
        <div class="card dark-card">
          <h3>How booking works</h3>
          <div class="stack">
            {#each checklist as item}
              <div class="check-row">
                <div class="check-num">{item.n}</div>
                <div>
                  <b>{item.title}</b>
                  <p>{item.text}</p>
                </div>
              </div>
            {/each}
          </div>
        </div>

        <form class="card quote-form" on:submit|preventDefault={handleQuoteSubmit}>
          {#if !submitted}
            <h3 class="form-title">Request car availability</h3>
            <div class="form-grid">
              <label>Your name<input required bind:value={quoteName} placeholder="Full name" /></label>
              <label>Mobile number<input required bind:value={quotePhone} placeholder="72182 83271" /></label>
              <label>Rental type
                <select bind:value={quoteType}>
                  <option>Car with driver</option>
                  <option>Airport transfer</option>
                  <option>Monthly rental</option>
                </select>
              </label>
              <label>Car category
                <select bind:value={quoteCar}>
                  <option>Hatchback</option>
                  <option>Sedan</option>
                  <option>SUV / MUV</option>
                  <option>Tempo Traveller</option>
                  <option>Premium</option>
                </select>
              </label>
              <label>Pickup date<input type="date" min={today} required bind:value={quoteDate} /></label>
              <label>Return date<input type="date" min={today} bind:value={quoteReturnDate} /></label>
              <label class="full">Route / usage<textarea rows="3" bind:value={quoteRoute} placeholder="Example: Pune to Goa for 3 days, or Pune local with driver for 8 hours"></textarea></label>
            </div>
            <button type="submit" class="btn primary submit-btn">Send booking request</button>
            <div class="muted small center">For faster booking, call 72182 83271 / +91 914663456 or WhatsApp your route details.</div>
          {:else}
            <div class="success">
              <div class="success-ico">✓</div>
              <h3>Request noted</h3>
              <p class="muted">Please call or WhatsApp us for immediate confirmation: 72182 83271 / +91 914663456.</p>
            </div>
          {/if}
        </form>
      </div>
    </div>
  </section>

  <section id="routes" class="section container">
    <div class="section-head">
      <div class="eyebrow accent">Popular routes</div>
      <h2 class="section-title">Pune rentals for Maharashtra and all India.</h2>
      <p class="muted">Use these as examples. We can quote local, round-trip, one-way, multi-city and long-duration rental plans depending on availability.</p>
    </div>

    <div class="grid routes-grid">
      <article class="card">
        <h3>High-demand routes from Pune</h3>
        <div class="route-list">
          {#each puneRoutes as r}
            <span class="route-pill">{r}</span>
          {/each}
        </div>
      </article>
      <article class="card">
        <h3>Cities We Serve</h3>
        <p class="muted">Travel comfortably across Maharashtra and India.</p>
        <div class="grid city-grid">
          {#each cities as city}
            <div class="city-card">
              <img src={city.image} alt={city.name} />
              <div class="city-overlay"></div>
              <h3>{city.name}</h3>
            </div>
          {/each}
        </div>
      </article>
    </div>
  </section>

  <section id="process" class="section">
    <div class="container">
      <div class="section-head">
        <div class="eyebrow accent">Simple booking flow</div>
        <h2 class="section-title">From enquiry to keys in four steps.</h2>
        <p class="muted">Rental customers want clarity before they pay. This section keeps the process visible: vehicle availability, fare, documents and handover.</p>
      </div>

      <div class="grid steps-grid">
        {#each steps as step}
          <article class="card step-card">
            <div class="step-num">{step.n}</div>
            <h3>{step.title}</h3>
            <p class="muted">{step.text}</p>
          </article>
        {/each}
      </div>

      <div class="card fare-card">
        <h3>Fare clarity before booking</h3>
        <ul>
          {#each fareList as f}
            <li>{f}</li>
          {/each}
        </ul>
      </div>
    </div>
  </section>

  <section id="why" class="section section-dark">
    <div class="container why-grid">
      <div class="card promise-card">
        <div class="eyebrow accent-light">The Shree Ram promise</div>
        <h2 class="promise-title">Clear fare</h2>
        <p class="muted light">No confusing package pricing. We focus on car rental needs: vehicle, route, dates, driver choice and final fare before confirmation.</p>
        <p class="muted light"><span class="stars">★★★★★</span><br />Built for Pune local, outstation customers.</p>
      </div>

      <div>
        <div class="eyebrow accent">Why customers choose us</div>
        <h2 class="section-title">Practical rental support, not just a booking form.</h2>
        <div class="why-list">
          {#each whyItems as item}
            <div class="why-item">
              <div class="why-icon">{item.icon}</div>
              <div>
                <h3>{item.title}</h3>
                <p class="muted">{item.text}</p>
              </div>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </section>

  <section id="reviews" class="section section-alt">
    <div class="container">
      <div class="section-head">
        <div class="eyebrow accent">Customer feedback</div>
        <h2 class="section-title">Made for daily, family and business travel.</h2>
      </div>

      <div class="grid reviews-grid">
        {#each reviews as r}
          <article class="card review-card">
            <div class="review-stars">★★★★★</div>
            <p class="muted">{r.text}</p>
            <div class="review-meta">
              <div class="review-badge">{r.initials}</div>
              <div>
                <b>{r.name}</b>
                <div class="muted small">{r.tag}</div>
              </div>
            </div>
          </article>
        {/each}
      </div>
    </div>
  </section>

  <section id="faq" class="section">
    <div class="container">
      <div class="section-head">
        <div class="eyebrow accent">Questions before booking</div>
        <h2 class="section-title">Quick answers for rental customers.</h2>
        <p class="muted">These FAQs reduce phone back-and-forth and make the site feel more trustworthy for first-time customers.</p>
      </div>

      <div class="grid faq-grid">
        {#each faqs as item}
          <article class="card faq-card">
            <h3>{item.q}</h3>
            <p class="muted">{item.a}</p>
          </article>
        {/each}
      </div>
    </div>
  </section>

  <footer class="footer">
    <div class="container footer-grid">
      <div>
        <a href="#" class="brand footer-brand"><span class="brand-mark">S</span><span>Shree Ram Travels</span></a>
        <p class="footer-muted">Car rentals services based in Pune, Maharashtra, serving routes across India.</p>
        <p class="footer-muted small">Office Pune, Maharashtra</p>
      </div>
      <div>
        <h4>Services</h4>
        <a href="#services">Car with driver</a>
        <a href="#services">Airport transfers</a>
        <a href="#services">Monthly rentals</a>
      </div>
      <div>
        <h4>Popular routes</h4>
        <a href="#routes">Pune to Mumbai</a>
        <a href="#routes">Pune to Goa</a>
        <a href="#routes">Pune to Shirdi</a>
      </div>
      <div>
        <h4>Contact</h4>
        <a href="tel:+917218283271">+91 72182 83271</a>
        <a href="tel:+91914663456">+91 914663456</a>
        <a href="mailto:contact@shreramtravel.com">contact@shreramtravel.com</a>
        <a href={waLink} target="_blank" rel="noopener">WhatsApp booking</a>
      </div>
    </div>

    <div class="container footer-bottom">
      <span class="footer-muted small">© 2026 Shree Ram Travels, Pune.</span>
      <span class="footer-muted small">Clean cars · Chauffeur-driven rentals · All-India outstation service</span>
    </div>
  </footer>

  <a href={waLink} target="_blank" rel="noopener" class="whatsapp">WhatsApp</a>
</main>

<style>
  :global(html) { scroll-behavior: smooth; }
  :global(body) { margin: 0; font-family: Inter, system-ui, sans-serif; background: #f5f7fb; color: #0f172a; }
  :global(*) { box-sizing: border-box; }
  :global(img) { max-width: 100%; display: block; }

  :root {
    --bg: #f5f7fb;
    --ink: #0f172a;
    --slate: #1e293b;
    --muted: #64748b;
    --card: #ffffff;
    --border: #dbe3ee;
    --accent: #c8a96a;
    --accent-soft: #f3ead7;
    --accent-dark: #9b7b35;
    --alt: #eef2f7;
    --shadow: 0 12px 30px rgba(15, 23, 42, 0.08);
  }

  main { overflow-x: hidden; }
  .container { width: min(1180px, calc(100% - 40px)); margin: 0 auto; }
  .section { padding: 80px 0; }
  .section-alt { background: var(--alt); }
  .section-dark { background: linear-gradient(180deg, #0f172a, #111c33); color: #fff; }
  .section-head { margin-bottom: 24px; }
  .light-head .muted, .light { color: rgba(255,255,255,0.72); }
  .eyebrow { text-transform: uppercase; letter-spacing: .14em; font-size: 12px; font-weight: 800; }
  .accent { color: var(--accent-dark); }
  .accent-light { color: #f3d9a3; }
  .section-title { font-size: clamp(2rem, 4.5vw, 3.65rem); line-height: 1.08; margin: 10px 0 0; font-weight: 800; letter-spacing: -.04em; }
  .muted { color: var(--muted); }
  .small { font-size: 13px; }
  .center { text-align: center; }
  .grid { display: grid; }
  .card { background: var(--card); border: 1px solid var(--border); border-radius: 28px; box-shadow: var(--shadow); }
  .btn { display: inline-flex; align-items: center; justify-content: center; gap: 8px; padding: 12px 18px; border-radius: 999px; text-decoration: none; font-weight: 800; border: 1px solid transparent; cursor: pointer; transition: transform .2s ease, opacity .2s ease; }
  .btn:hover { transform: translateY(-1px); }
  .btn.primary { background: linear-gradient(135deg, var(--accent), #e2c78d); color: #1b1b1b; }
  .btn.ghost { background: transparent; border-color: rgba(255,255,255,.18); color: #fff; }
  .btn.ghost.light { border-color: var(--border); color: var(--ink); background: #fff; }
  .brand { display: inline-flex; align-items: center; gap: 10px; color: inherit; text-decoration: none; font-weight: 900; }
  .brand-mark { width: 40px; height: 40px; border-radius: 12px; background: var(--accent); color: #fff; display: grid; place-items: center; }

  .topbar { background: #0b1222; color: #fff; padding: 10px 0; font-size: 13px; }
  .topbar-inner { display: flex; flex-wrap: wrap; justify-content: center; gap: 18px; align-items: center; }
  .dot { width: 8px; height: 8px; border-radius: 50%; background: #69d19a; display: inline-block; }
  .header { position: relative; z-index: 20; }
  .nav { height: 82px; display: flex; align-items: center; justify-content: space-between; }
  .nav-links { display: flex; gap: 18px; align-items: center; }
  .nav-links a { text-decoration: none; color: var(--ink); font-weight: 700; }
  .nav-actions { display: flex; gap: 10px; align-items: center; }
  .menu-btn { display: none; border: 0; background: var(--card); border-radius: 12px; padding: 10px 12px; font-size: 18px; }

  .hero { min-height: 700px; display: flex; align-items: center; color: #fff; background: linear-gradient(90deg, rgba(15,23,42,.93), rgba(15,23,42,.74) 45%, rgba(15,23,42,.25) 76%), url('/images/s.png') center/cover no-repeat; }
  .hero-inner { display: grid; grid-template-columns: 1.2fr .95fr; gap: 28px; align-items: center; padding: 70px 0; }
  .hero-copy h1 { font-size: clamp(2.8rem, 8vw, 6.2rem); line-height: .95; margin: 14px 0 16px; letter-spacing: -.05em; }
  .hero-copy em { font-style: italic; color: #f3d9a3; }
  .hero-copy p { max-width: 650px; color: rgba(255,255,255,.84); font-size: 1.05rem; }
  .actions { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 22px; }
  .trust { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 22px; color: rgba(255,255,255,.82); font-size: .95rem; }

  .quick-card { background: #fff; color: var(--ink); border-radius: 28px; padding: 16px; box-shadow: var(--shadow); display: grid; gap: 10px; }
  .quick-card label, .quote-form label { display: grid; gap: 8px; font-size: 12px; font-weight: 800; text-transform: uppercase; letter-spacing: .08em; color: var(--muted); }
  .quick-card input, .quick-card select, .quote-form input, .quote-form select, .quote-form textarea { width: 100%; border: 1px solid var(--border); background: #fff; border-radius: 14px; padding: 13px 14px; color: var(--ink); font: inherit; text-transform: none; letter-spacing: normal; }
  .wide { width: 100%; }

  .metrics { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1px; background: var(--border); margin-top: -36px; border-radius: 22px; overflow: hidden; position: relative; z-index: 2; }
  .metric { background: #fff; text-align: center; padding: 26px 18px; }
  .metric b { display: block; font-size: 1.45rem; }
  .metric span { color: var(--muted); font-size: .92rem; }

  .about-grid { grid-template-columns: 1fr .95fr; gap: 22px; }
  .about-card, .promise-list, .service-card, .car-card, .quote-form, .dark-card, .review-card, .faq-card, .fare-card, .step-card { padding: 26px; }
  .promise-list { display: grid; gap: 14px; }
  .promise-item { display: grid; grid-template-columns: 46px 1fr; gap: 14px; align-items: start; }
  .promise-num, .step-num, .check-num { width: 46px; height: 46px; border-radius: 16px; display: grid; place-items: center; font-weight: 900; background: rgba(200,169,106,.15); color: var(--accent-dark); }
  .pills { display: flex; gap: 10px; flex-wrap: wrap; margin-top: 18px; }
  .pill, .meta-item, .route-pill { background: #f3ead7; color: #6f5721; border: 1px solid rgba(155,123,53,.16); border-radius: 999px; padding: 10px 12px; font-size: 13px; font-weight: 800; }

  .services-grid { grid-template-columns: repeat(4, 1fr); gap: 16px; }
  .service-card { display: grid; gap: 10px; }
  .service-icon { width: 58px; height: 58px; border-radius: 16px; background: #f3ead7; display: grid; place-items: center; font-size: 1.5rem; }

  .tabs { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 18px; }
  .tab { border: 1px solid var(--border); background: transparent; border-radius: 999px; padding: 10px 14px; font-weight: 800; cursor: pointer; color: var(--muted); }
  .tab.active { background: var(--ink); color: #fff; border-color: var(--ink); }
  .cars-grid { grid-template-columns: repeat(3, 1fr); gap: 20px; }
  .car-card { overflow: hidden; padding: 0; }
  .car-hero { height: 230px; background: linear-gradient(135deg, #1f2937, #0f172a); display: grid; place-items: center; position: relative; color: #fff; font-size: 5rem; }
  .car-badge { position: absolute; left: 14px; top: 14px; background: #fff; color: var(--ink); border-radius: 999px; padding: 8px 12px; font-size: 12px; font-weight: 900; }
  .card-body { padding: 22px 24px 24px; }
  .car-title, .service-card h3, .promise-item h3, .review-card b, .faq-card h3, .card h3, .step-card h3, .dark-card h3 { margin: 0 0 6px; font-size: 1.2rem; }
  .car-title { font-size: 1.35rem; }
  .meta { display: flex; flex-wrap: wrap; gap: 8px; margin: 16px 0; }
  .card-footer { display: flex; justify-content: space-between; align-items: end; border-top: 1px solid var(--border); padding-top: 18px; margin-top: 10px; }
  .price { display: block; font-size: 1.7rem; }
  .link { color: var(--accent-dark); text-decoration: none; font-weight: 900; }

  .quote-grid { grid-template-columns: 1fr .96fr; gap: 20px; align-items: start; }
  .dark-card { background: rgba(255,255,255,.05); border-color: rgba(255,255,255,.08); color: #fff; }
  .dark-card p { color: rgba(255,255,255,.7); }
  .stack { display: grid; gap: 14px; margin-top: 18px; }
  .check-row { display: grid; grid-template-columns: 46px 1fr; gap: 12px; align-items: start; }
  .check-row p { margin: 6px 0 0; }
  .quote-form { background: #fff; }
  .form-title { margin: 0 0 16px; font-size: 1.4rem; }
  .form-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
  .full { grid-column: 1 / -1; }
  .submit-btn { margin-top: 8px; }
  .success { text-align: center; padding: 24px 0; }
  .success-ico { width: 58px; height: 58px; border-radius: 50%; margin: 0 auto 12px; display: grid; place-items: center; background: #e8f7ef; color: #15803d; font-size: 1.5rem; font-weight: 900; }

  .routes-grid { grid-template-columns: 1fr 1fr; gap: 18px; }
  .route-list { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 14px; }
  .city-grid { grid-template-columns: repeat(3, 1fr); gap: 14px; margin-top: 14px; }
  .city-card { position: relative; overflow: hidden; border-radius: 20px; min-height: 190px; }
  .city-card img { width: 100%; height: 100%; object-fit: cover; }
  .city-overlay { position: absolute; inset: 0; background: linear-gradient(to top, rgba(0,0,0,.72), rgba(0,0,0,.12)); }
  .city-card h3 { position: absolute; left: 0; right: 0; bottom: 16px; text-align: center; color: #fff; font-size: 1.6rem; margin: 0; }

  .steps-grid { grid-template-columns: repeat(4, 1fr); gap: 14px; }
  .fare-card { margin-top: 18px; }
  .fare-card ul { margin: 14px 0 0; padding-left: 20px; color: var(--muted); line-height: 1.8; }

  .why-grid { grid-template-columns: .9fr 1.1fr; gap: 22px; align-items: center; }
  .promise-card { background: linear-gradient(180deg, #111827, #0f172a); color: #fff; position: relative; overflow: hidden; }
  .promise-card:after { content: ''; position: absolute; width: 240px; height: 240px; border-radius: 50%; background: rgba(200,169,106,.35); right: -90px; bottom: -90px; }
  .promise-title { font-size: clamp(2.8rem, 6vw, 4.5rem); margin: 10px 0; }
  .stars { color: #f3d9a3; }
  .why-list { display: grid; gap: 14px; margin-top: 20px; }
  .why-item { display: grid; grid-template-columns: 48px 1fr; gap: 14px; align-items: start; }
  .why-icon { width: 48px; height: 48px; border-radius: 16px; background: #f3ead7; display: grid; place-items: center; font-size: 1.1rem; }

  .reviews-grid { grid-template-columns: repeat(3, 1fr); gap: 16px; }
  .review-stars { color: var(--accent-dark); margin-bottom: 10px; }
  .review-meta { display: flex; gap: 12px; align-items: center; margin-top: 16px; }
  .review-badge { width: 42px; height: 42px; border-radius: 50%; background: #f3ead7; color: var(--accent-dark); display: grid; place-items: center; font-weight: 900; }

  .faq-grid { grid-template-columns: repeat(2, 1fr); gap: 14px; }

  .footer { background: #0b1222; color: #fff; padding: 48px 0 22px; }
  .footer-grid { grid-template-columns: 1.2fr 1fr 1fr 1fr; gap: 22px; }
  .footer a { color: rgba(255,255,255,.8); text-decoration: none; display: block; margin: 8px 0; }
  .footer-brand { color: #fff; margin-bottom: 12px; }
  .footer-muted { color: rgba(255,255,255,.65); }
  .footer-bottom { display: flex; justify-content: space-between; gap: 12px; border-top: 1px solid rgba(255,255,255,.08); margin-top: 20px; padding-top: 16px; }

  .whatsapp { position: fixed; right: 18px; bottom: 18px; width: 58px; height: 58px; border-radius: 50%; background: #25d366; color: #fff; display: grid; place-items: center; text-decoration: none; font-weight: 900; box-shadow: 0 12px 28px rgba(0,0,0,.22); z-index: 40; }
  .desktop-only { display: flex; }

  @media (max-width: 1024px) {
    .hero-inner, .about-grid, .quote-grid, .why-grid, .routes-grid, .footer-grid { grid-template-columns: 1fr; }
    .services-grid, .cars-grid, .reviews-grid, .steps-grid { grid-template-columns: repeat(2, 1fr); }
    .city-grid { grid-template-columns: repeat(2, 1fr); }
    .nav-links { display: none; position: absolute; left: 20px; right: 20px; top: 82px; background: #111827; color: #fff; padding: 16px; border-radius: 18px; flex-direction: column; align-items: flex-start; }
    .nav-links.open { display: flex; }
    .nav-links a { color: #fff; padding: 8px 0; }
    .menu-btn { display: inline-flex; }
    .desktop-only { display: none; }
    .hero { min-height: auto; }
  }

  @media (max-width: 640px) {
    .section { padding: 64px 0; }
    .metrics, .services-grid, .cars-grid, .reviews-grid, .faq-grid, .steps-grid, .city-grid, .form-grid { grid-template-columns: 1fr; }
    .topbar-inner { gap: 10px; }
    .footer-bottom { flex-direction: column; }
    .hero-copy h1 { font-size: 2.8rem; }
  }
</style>