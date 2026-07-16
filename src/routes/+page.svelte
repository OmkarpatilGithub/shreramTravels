<script>
  // ---------- Mobile nav ----------
  let menuOpen = false;
  let fabOpen = false;

  const phoneNumber = "+91 7218283271";
  // ---------- Quick booking strip (hero) ----------
  let quickType = "With driver";
  let quickPickup = "Pune, Maharashtra";
  let quickDrop = "";

  // ---------- Quote form (self-drive section) ----------
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
    quoteRoute = `${quickPickup} - ${quickDrop}`;
    document.getElementById("quote")?.scrollIntoView({ behavior: "smooth" });
  }

  function handleQuoteSubmit(e) {
    e.preventDefault();
    submitted = true;
  }

  // ---------- Fleet filter ----------
  let activeFilter = "all";
  const tabs = [
    { label: "All cars", value: "all" },
    // { label: "Self-drive", value: "self" },
    { label: "With driver", value: "driver" },
    { label: "Group travel", value: "group" },
  ];

  const cars = [
    {
      types: ["self", "driver"],
      badge: "Budget friendly",
      emoji: "🚙",
      title: "Hatchback",
      desc: "Swift, i20 or similar. Best for city use and short self-drive plans.",
      meta: ["4 seats", "AC", "Self-drive"],
      priceLabel: "from",
      price: "₹1,899/day",
    },
    {
      types: ["self", "driver"],
      badge: "Most popular",
      emoji: "🚘",
      title: "Sedan",
      desc: "Dzire, Aura or similar. Comfortable for Pune-Mumbai, Mahabaleshwar and business trips.",
      meta: ["4 seats", "Large boot", "Driver option"],
      priceLabel: "from",
      price: "₹12/km",
    },
    {
      types: ["self", "driver"],
      badge: "Family choice",
      emoji: "🚐",
      title: "SUV / MUV",
      desc: "Ertiga, Innova or similar. Ideal for family trips, luggage and long highway drives.",
      meta: ["6-7 seats", "AC", "Outstation"],
      priceLabel: "from",
      price: "₹17/km",
    },
    {
      types: ["group", "driver"],
      badge: "Group travel",
      emoji: "🚌",
      title: "Tempo Traveller",
      desc: "12 to 17 seater vehicles for office outings, weddings, pilgrimage and group tours.",
      meta: ["12-17 seats", "Driver", "Luggage space"],
      priceLabel: "from",
      price: "₹24/km",
    },
    {
      types: ["self", "driver"],
      badge: "Premium",
      emoji: "🏎️",
      title: "Luxury cars",
      desc: "Premium sedans and SUVs for weddings, VIP movement, corporate guests and special days.",
      meta: ["Premium", "On request", "Driver option"],
      priceLabel: "custom",
      price: "Get quote",
    },
    {
      types: ["driver"],
      badge: "Airport ready",
      emoji: "🚕",
      title: "Airport cab",
      desc: "Dedicated pickup and drop service for Pune Airport, Mumbai Airport and railway stations.",
      meta: ["On time", "AC", "Local support"],
      priceLabel: "from",
      price: "₹999",
    },
  ];

  $: visibleCars = cars.filter(
    (c) => activeFilter === "all" || c.types.includes(activeFilter),
  );

  // ---------- Content data ----------
  const aboutPoints = [
    {
      n: "01",
      title: "Right vehicle for the route",
      text: "Compact cars for city use, sedans for business travel, SUVs for family trips, and tempo travellers for groups.",
    },
    {
      n: "02",
      title: "Rental terms explained upfront",
      text: "Fare, kilometre limits, tolls, parking, fuel policy, deposit and driver allowance are discussed before confirmation.",
    },
    {
      n: "03",
      title: "Direct Pune contact",
      text: "Customers can call or WhatsApp directly instead of dealing with a faceless marketplace or delayed callback system.",
    },
  ];

  const services = [
    // {
    //   icon: "🚗",
    //   title: "Self-drive Cars",
    //   text: "Coming Soon",
    // },
    {
      icon: "👨‍✈️",
      title: "Car with driver",
      text: "Verified drivers for local sightseeing, meetings, events, family functions and outstation routes.",
    },
    {
      icon: "✈️",
      title: "Airport transfer",
      text: "Pune Airport, Mumbai Airport and railway-station pickups with clean vehicles and punctual reporting.",
    },
    {
      icon: "📅",
      title: "Monthly rentals",
      text: "Company staff transport, executive cars and long-term vehicle needs with custom monthly pricing.",
    },
  ];

  const checklist = [
    {
      n: 1,
      title: "Share dates and car type",
      text: "Tell us your pickup date, return date, route and preferred vehicle category.",
    },
    // {
    //   n: 2,
    //   title: "Verify documents",
    //   text: "Valid driving licence, ID proof and refundable security deposit may be required.",
    // },
    {
      n: 2,
      title: "Get a clear rental plan",
      text: "We confirm fare, kilometre limit, fuel policy, pickup point and support contact before booking.",
    },
    {
      n: 3,
      title: "Drive with support",
      text: "Our Pune desk stays reachable for route help, extension requests and roadside coordination.",
    },
  ];

const routeGroups = [
  {
    state: "Maharashtra",
    routes: [
      "Pune → Mumbai",
      "Pune → Nashik",
      "Pune → Shirdi",
      "Pune → Kolhapur",
      "Pune → Ratnagiri",
      "Pune → Ganpatipule",
      "Pune → Mahabaleshwar",
      "Pune → Lonavala",
    ]
  },
  {
    state: "Goa",
    routes: [
      "Pune → Panaji",
      "Pune → Calangute",
      "Pune → Baga",
      "Pune → Candolim",
      "Pune → Vasco da Gama"
    ]
  },
  {
    state: "Karnataka",
    routes: [
      "Pune → Bengaluru",
      "Pune → Mysuru",
      "Pune → Hubballi",
      "Pune → Belagavi",
      "Pune → Hampi"
    ]
  },
  {
    state: "Gujarat",
    routes: [
      "Pune → Ahmedabad",
      "Pune → Surat",
      "Pune → Vadodara",
      "Pune → Rajkot",
      "Pune → Dwarka"
    ]
  },
  {
    state: "Madhya Pradesh",
    routes: [
      "Pune → Indore",
      "Pune → Bhopal",
      "Pune → Ujjain",
      "Pune → Gwalior"
    ]
  },
  {
    state: "Rajasthan",
    routes: [
      "Pune → Jaipur",
      "Pune → Udaipur",
      "Pune → Jodhpur",
      "Pune → Mount Abu"
    ]
  },
  {
    state: "Delhi",
    routes: [
      "Pune → New Delhi",
      "Pune → Gurugram",
      "Pune → Noida"
    ]
  },
  {
    state: "Uttar Pradesh",
    routes: [
      "Pune → Agra",
      "Pune → Varanasi",
      "Pune → Lucknow",
      "Pune → Prayagraj"
    ]
  },
  {
    state: "Uttarakhand",
    routes: [
      "Pune → Dehradun",
      "Pune → Haridwar",
      "Pune → Rishikesh",
      "Pune → Nainital"
    ]
  },
  {
    state: "Himachal Pradesh",
    routes: [
      "Pune → Shimla",
      "Pune → Manali",
      "Pune → Dharamshala"
    ]
  },
  {
    state: "Jammu & Kashmir",
    routes: [
      "Pune → Srinagar",
      "Pune → Gulmarg",
      "Pune → Jammu"
    ]
  },
  {
    state: "Tamil Nadu",
    routes: [
      "Pune → Chennai",
      "Pune → Coimbatore",
      "Pune → Madurai",
      "Pune → Ooty"
    ]
  },
  {
    state: "Kerala",
    routes: [
      "Pune → Kochi",
      "Pune → Munnar",
      "Pune → Alleppey",
      "Pune → Thiruvananthapuram"
    ]
  },
  {
    state: "Andhra Pradesh",
    routes: [
      "Pune → Tirupati",
      "Pune → Visakhapatnam",
      "Pune → Vijayawada"
    ]
  },
  {
    state: "Telangana",
    routes: [
      "Pune → Hyderabad",
      "Pune → Warangal"
    ]
  }
]; 
const cities = [
    { name: "Pune", image: "/pune.png" },
    { name: "Mumbai", image: "/mumbai.png" },
    { name: "Goa", image: "/goa.png" },
    { name: "Nashik", image: "/nashik.png" },
    { name: "Shirdi", image: "/shirdi.png" },
    { name: "Lonavala", image: "/lonavala.png" }
]; 

  const steps = [
    {
      n: 1,
      title: "Send trip details",
      text: "Share rental type, pickup city, destination or usage, dates, car category and driver preference.",
    },
    {
      n: 2,
      title: "Get vehicle options",
      text: "We confirm available cars, seating, luggage suitability, estimated fare and pickup reporting time.",
    },
    {
      n: 3,
      title: "Confirm documents",
      text: "For self-drive, we verify licence and ID. For driver rentals, we confirm route, tolls, parking and allowance terms.",
    },
    {
      n: 4,
      title: "Start your rental",
      text: "Receive car details, support number and final checklist before pickup or driver reporting.",
    },
  ];

  const docsList = [
    "Valid driving licence",
    "Aadhaar / PAN / passport ID proof",
    "Current address proof if required",
    "Refundable security deposit as per vehicle",
    "Customer must follow agreed fuel, kilometre and return terms",
  ];

  const fareList = [
    "Vehicle category and rental duration",
    "Per-km or per-day rate, depending on service",
    "Driver allowance for outstation rentals when applicable",
    "Toll, parking, state tax and permit handling explained upfront",
    "Fuel policy and extra-km charges explained before confirmation",
  ];

  const whyItems = [
    {
      icon: "✓",
      title: "Vehicle options for every use",
      text: "Driver cars, airport cabs, SUVs, tempo travellers and premium cars from one provider.",
    },
    {
      icon: "₹",
      title: "Transparent quotes",
      text: "We explain per-km charges, day limits, toll/parking, driver allowance and deposit terms clearly.",
    },
    {
      icon: "☎",
      title: "Direct owner-style contact",
      text: "Call or WhatsApp the Pune team directly instead of waiting for a generic marketplace response.",
    },
  ];

  const reviews = [
    {
      text: '"Booked a Pune to Mumbai cab at short notice. Clean car, clear fare and the driver reported on time."',
      initials: "AG",
      name: "Amit G.",
      tag: "Outstation rental",
    },
    {
      text: '"We used an Mini Traveler for a family trip from Pune to Goa. Good vehicle condition and helpful support throughout."',
      initials: "PR",
      name: "Priya R.",
      tag: "Family Trip ",
    },
    {
      text: '"We used an SUV for a family trip from Pune. Good vehicle condition and helpful support throughout."',
      initials: "SK",
      name: "Sachin K.",
      tag: "Family Trip",
    },
  ];

  const faqs = [
    {
      q: "Do you provide self-drive cars from Pune?",
      a: "NO, self-drive cars are currently Not available.",
    },
    {
      q: "Can I book a car with driver for outstation trips?",
      a: "Yes. We provide chauffeur-driven cars for Pune local, one-way, round-trip and multi-city outstation rentals across India.",
    },
    {
      q: "Are tolls and parking included?",
      a: "It depends on the route and rental plan. We explain tolls, parking, state tax, permit and driver allowance before confirmation.",
    },
    {
      q: "How fast can I confirm a booking?",
      a: "For urgent bookings, call or WhatsApp 72182 83271. Availability depends on date, route, vehicle category and rental type.",
    },
    {
      q: "Do you offer monthly or corporate rentals?",
      a: "Yes. Monthly rentals, executive cars and company transport can be quoted based on vehicle type, daily usage and reporting location.",
    },
    {
      q: "Which areas do you serve?",
      a: "We are based in Pune, Maharashtra and support local, airport, Maharashtra outstation and all-India rental requirements.",
    },
  ];

  const waLink =
    "https://wa.me/9146634563?text=Hello%20Shree%20Ram%20Travels%2C%20I%20need%20a%20car%20rental%20quote.";
  
  
   const waLink1 =
    "https://wa.me/7218283271?text=Hello%20Shree%20Ram%20Travels%2C%20I%20need%20a%20car%20rental%20quote.";
 
</script>

<main class="font-sans text-ink bg-cream">
  <!-- Topbar -->
  <div class="bg-black text-white text-sm py-2">
    <div
      class="w-[min(1180px,calc(100%-40px))] mx-auto flex flex-wrap justify-center gap-7"
    >
      <span class="flex items-center"
        ><span
          class="w-[7px] h-[7px] rounded-full bg-[#63e0ae] inline-block mr-2"
        ></span>Pune, Maharashtra based</span
      >
      <span>Cars across India</span>
      <span>Call: +91 7218283271 / +91 9146634563</span>
    </div>
  </div>

  <!-- Header / Nav -->
  <header
    class="relative md:absolute left-0 top-0 md:top-9 w-full z-20 bg-transparent text-black border-b border-white/20 " 
  >
    <nav
      class="w-[min(1180px,calc(100%-40px))] mx-auto h-[82px] flex items-center justify-between"
    >
      <a
        href="#"
        class="font-display font-extrabold text-xl  flex items-center gap-2.5"
      >
        <span
          class="w-10 h-10 rounded-full grid place-items-center bg-orange-400 text-white text-sm font-sans"
          >श्री</span
        >
        <span class="md:text-white">        Shree Ram Travels </span>

      </a>

      <div
        class={`flex-col items-start gap-0 font-bold text-sm bg-gray-300 p-5 rounded-2xl absolute top-[82px] left-5 right-5 md:static md:flex md:flex-row md:text-white md:bg-transparent md:p-0 md:rounded-none md:items-center md:gap-7 ${menuOpen ? "flex" : "hidden"}`}
      >
        <a href="#about" class="py-2 md:py-0">About</a>
        <a href="#services" class="py-2 md:py-0">Services</a>
        <a href="#fleet" class="py-2 md:py-0">Fleet</a>
       
        <a href="#process" class="py-2 md:py-0">Process</a>
        <a href="#routes" class="py-2 md:py-0">Routes</a>
        <a href="#faq" class="py-2 md:py-0">FAQ</a>
        <a href="#why" class="py-2 md:py-0">Why us</a>
      </div>

      <div class="hidden md:flex gap-2.5 items-center">
        <a
          href="tel:+917218283271"
          class="border-0 rounded-full px-5 py-3 font-extrabold inline-flex items-center gap-2 transition hover:-translate-y-0.5 bg-white/10 border border-white/35 text-white"
          >Call now</a
        >
        <a
          href="#quote"
          class="border-0 rounded-full px-5 py-3 font-extrabold inline-flex items-center gap-2 transition hover:-translate-y-0.5 bg-orange text-white shadow-[0_12px_25px_rgba(240,100,59,.25)]"
          >Book a car</a
        >
      </div>

      <button
        class="md:hidden border-0 rounded-xl px-3 py-2.5 bg-black text-white"
        aria-label="Open menu"
        on:click={() => (menuOpen = !menuOpen)}>☰</button
      >
    </nav>
  </header>

  <!-- Hero -->
  <section
    class="min-h-[600px] md:min-h-[780px] pt-16 md:pt-[120px] text-white flex items-center bg-cover bg-center"
    style="background-image: linear-gradient(90deg, rgba(8,31,42,.93) 0%, rgba(8,31,42,.74) 43%, rgba(8,31,42,.2) 76%), url('/imagess.png');"
  >
    <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
      <div class="w-full md:w-[min(710px,100%)]">
        <div
          class="text-xs font-extrabold tracking-[.14em] uppercase text-[#a7f1d0]"
        >
          Car rentals from Pune across India
        </div>
        <h1
          class="font-display mt-4 mb-5 tracking-[-.045em] text-[clamp(2.4rem,7vw,6.4rem)] leading-[0.95] md:leading-[.91]"
        >
          Pune car rentals, <em
            class="font-serif italic font-normal text-[#ffbd9d] not-italic md:italic"
            >done clearly.</em
          >
        </h1>
        <p class="text-lg text-white/85 max-w-[610px] mb-7">
          Book chauffeur-driven vehicles from Shree Ram
          Travels for Pune local travel, airport transfers, outstation routes,
          one-way drops and monthly business use across India.
        </p>
        <div class="flex gap-3 flex-wrap">
          <a
            href="#quote"
            class="border-0 rounded-full px-5 py-3 font-extrabold inline-flex items-center gap-2 transition hover:-translate-y-0.5 bg-orange text-white shadow-[0_12px_25px_rgba(240,100,59,.25)]"
            >Get instant quote</a
          >
          <a
            href={waLink}
            target="_blank"
            rel="noopener"
            class="border-0 rounded-full px-5 py-3 font-extrabold inline-flex items-center gap-2 transition hover:-translate-y-0.5 bg-white/10 border border-white/35 text-white"
            >WhatsApp us</a
          >
        </div>
        <div
          class="flex gap-4 items-center mt-7 text-white/85 text-sm flex-wrap"
        >
          <span
            ><span class="text-[#ffc65b] tracking-wide">★★★★★</span><br
            />Trusted by Pune families, renters and businesses</span
          >
          <span>✓ Clean cars</span>
          <span>✓ Transparent fare</span>
          <span>✓ 24×7 road support</span>
        </div>
      </div>
    </div>
  </section>

  <div class="w-[min(1180px,calc(100%-40px))] mt-10 mx-auto ">
    <!-- Metric row -->
    <div
      class="relative z-10 mt-6 bg-white rounded-3xl p-4 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-[1fr_1fr_1fr_auto] gap-2 border shadow-brand"
    >
      <div class="p-3.5 border-b sm:border-b-0 md:border-r border-line">
        <b class="font-display text-2xl block">24×7</b>
        <span class="text-sm text-muted">booking and trip support</span>
      </div>
      <div class="p-3.5 border-b sm:border-b-0 md:border-r border-line">
        <b class="font-display text-2xl block">All India</b>
        <span class="text-sm text-muted">outstation service routes</span>
      </div>
      <div class="p-3.5 border-b sm:border-b-0 md:border-r border-line">
        <b class="font-display text-2xl block">Pune</b>
        <span class="text-sm text-muted">pickup and local expertise</span>
      </div>
      <div class="p-3.5">
        <b class="font-display text-2xl block">Self-drive</b>
        <span class="text-sm text-muted">Coming Soon</span>
      </div>
    </div>

    <!-- Quick booking card -->
    <form
      class="relative z-10 mt-6 bg-white rounded-3xl p-4 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-[1fr_1fr_1fr_auto] gap-2 border shadow-brand"
      on:submit={handleQuickSubmit}
    >
      <div class="p-3.5 border-b sm:border-b-0 md:border-r border-line">
        <label
          class="block text-xs uppercase tracking-wide font-extrabold text-muted mb-1.5"
          for="quickType">Rental type</label
        >
        <select
          id="quickType"
          bind:value={quickType}
          class="border-0 outline-none w-full font-extrabold text-ink bg-white"
        >
          <!-- <option>Self-drive car</option> -->
          <option>With driver</option>
          <option>Airport transfer</option>
          <option>Monthly rental</option>
        </select>
      </div>
      <div class="p-3.5 border-b sm:border-b-0 md:border-r border-line">
        <label
          class="block text-xs uppercase tracking-wide font-extrabold text-muted mb-1.5"
          for="quickPickup">Pickup city</label
        >
        <input
          id="quickPickup"
          bind:value={quickPickup}
          class="border-0 outline-none w-full font-extrabold text-ink bg-white"
        />
      </div>
      <div class="p-3.5 border-b sm:border-b-0 md:border-r border-line">
        <label
          class="block text-xs uppercase tracking-wide font-extrabold text-muted mb-1.5"
          for="quickDrop">Destination / usage</label
        >
        <input
          id="quickDrop"
          bind:value={quickDrop}
          placeholder="Mumbai, Goa, local Pune, etc."
          class="border-0 outline-none w-full font-extrabold text-ink bg-white placeholder:font-medium"
        />
      </div>
      <button
        type="submit"
        class="border-0 rounded-2xl px-5 py-3 font-extrabold inline-flex items-center justify-center gap-2 transition hover:-translate-y-0.5 bg-orange-300 text-white shadow-[0_12px_25px_rgba(240,100,59,.25)] min-w-[160px] col-span-1 sm:col-span-2 md:col-span-1"
        >Check availability →</button
      >
    </form>
  </div>

  <!-- About -->
  <section id="about" class="py-16 md:py-24">
    <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
      <div
        class="grid grid-cols-1 lg:grid-cols-[1.05fr_.95fr] gap-6 items-stretch"
      >
        <div
          class="bg-white border border-line rounded-[28px] p-8 shadow-[0_10px_30px_rgba(8,31,42,.05)]"
        >
          <div
            class="text-xs font-extrabold tracking-[.14em] uppercase text-teal"
          >
            About Shree Ram Travels
          </div>
          <h2
            class="font-display tracking-[-.045em] text-[clamp(1.8rem,4.5vw,3.65rem)] leading-tight mt-2"
          >
            Pune-based car rental service with an all-India mindset.
          </h2>
          <p class="text-muted mt-4">
            Shree Ram Travels is built for people who need a dependable vehicle
            without confusion: families planning outstation travel,
            professionals moving between cities, visitors landing at Pune or
            Mumbai airport.
          </p>
          <p class="text-muted mt-4">
            Our work is simple: understand the route, suggest the right car,
            explain the fare clearly, and stay reachable during the rental.
            Whether it is Pune local use, a Maharashtra weekend route, a one-way
            airport drop, or a longer all-India journey, the booking starts with
            direct human support.
          </p>
          <div class="grid grid-cols-2 md:grid-cols-4 gap-3 mt-6">
            <div
              class="bg-[#f2f8f5] border border-line rounded-2xl p-3.5 font-extrabold text-[#36595d] text-sm"
            >
              Pune local rentals
            </div>
            <!-- <div
              class="bg-[#f2f8f5] border border-line rounded-2xl p-3.5 font-extrabold text-[#36595d] text-sm"
            >
              Self-drive cars
            </div> -->
            <div
              class="bg-[#f2f8f5] border border-line rounded-2xl p-3.5 font-extrabold text-[#36595d] text-sm"
            >
              Outstation cabs
            </div>
            <div
              class="bg-[#f2f8f5] border border-line rounded-2xl p-3.5 font-extrabold text-[#36595d] text-sm"
            >
              Corporate monthly cars
            </div>
          </div>
        </div>
        <div class="bg-[#eef7f3] text-white rounded-[28px] p-7 grid gap-3.5">
          {#each aboutPoints as point}
            <div
              class="grid grid-cols-[46px_1fr] gap-3.5 items-start bg-white border border-white/10 rounded-2xl p-4"
            >
              <i
                class="w-[46px] h-[46px] rounded-2xl bg-[#a7f1d0] grid place-items-center not-italic text-black font-extrabold"
                >{point.n}</i
              >
              <div>
                <h3 class="text-xl text-black font-bold">{point.title}</h3>
                <p class="mt-1 text-black text-sm">{point.text}</p>
              </div>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </section>
<section>
     <article class="bg-white rounded-3xl p-7 border border-line">
           <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
        <div class="text-center mb-10">
            <h2 class="font-display text-5xl">
                Cities We Serve
            </h2>
            <p class="text-muted mt-3">
                Travel comfortably across Maharashtra and India.
            </p>
        </div>

      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
    {#each cities as city}
        <div class="relative overflow-hidden rounded-3xl shadow-lg group">
            <img
                src={city.image}
                alt={city.name}
                class="h-72 w-full object-cover transition duration-500 group-hover:scale-110"
            />

            <div class="absolute inset-0 bg-gradient-to-t from-white/70 via-black/20 to-transparent"></div>

            <h3 class="absolute bottom-5 left-0 right-0 text-center text-white text-3xl font-display font-bold tracking-wide">
                {city.name}
            </h3>
        </div>
    {/each}
</div>
          <!-- <h3 class="text-xl font-display">All-India service examples</h3> -->
          <!-- <div class="grid grid-cols-1 sm:grid-cols-2 gap-2.5 mt-4.5">
            {#each cities as r}
              <span
                class="bg-[#f2f8f5] border border-line rounded-xl p-3 font-extrabold text-[#36595d]"
                >{r}</span
              >
            {/each}
          </div> -->
        </article>
</section>
  <!-- Services -->
  <section id="services" class="py-16 md:py-24">
    <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
      <div
        class="flex flex-col md:flex-row md:justify-between md:items-end gap-7 mb-9"
      >
        <div>
          <div
            class="text-xs font-extrabold tracking-[.14em] uppercase text-teal"
          >
            What we offer
          </div>
          <h2
            class="font-display tracking-[-.045em] text-[clamp(2rem,4.5vw,3.65rem)] leading-tight mt-2"
          >
            Car rental services built for real Indian roads.
          </h2>
        </div>
        <p class="max-w-[500px] text-muted">
          Focused only on rentals: no package clutter. Pick the service you
          need, get a clear fare, and travel with support from our Pune team.
        </p>
      </div>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
        {#each services as s}
          <article
            class="bg-white border border-line rounded-[22px] p-6 transition duration-300 hover:-translate-y-1 hover:shadow-brand"
          >
            <div
              class="w-[52px] h-[52px] rounded-2xl bg-mint grid place-items-center text-2xl mb-4.5"
            >
              {s.icon}
            </div>
            <h3 class="text-xl font-display">{s.title}</h3>
            <p class="text-muted text-sm mt-2.5">{s.text}</p>
          </article>
        {/each}
      </div>
    </div>
  </section>

  <!-- Fleet -->
  <section class="bg-[#eef7f3] py-16 md:py-24" id="fleet">
    <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
      <div
        class="flex flex-col md:flex-row md:justify-between md:items-end gap-7 mb-9"
      >
        <div>
          <div
            class="text-xs font-extrabold tracking-[.14em] uppercase text-teal"
          >
            Choose your car
          </div>
          <h2
            class="font-display tracking-[-.045em] text-[clamp(2rem,4.5vw,3.65rem)] leading-tight mt-2"
          >
            Fleet options for driver rentals.
          </h2>
        </div>
        <p class="max-w-[500px] text-muted">
          Rates shown are sample starting prices for presentation. Final fare
          depends on car availability, route, dates, fuel plan and rental
          duration.
        </p>
      </div>

      <div class="flex gap-2 flex-wrap mb-6">
        {#each tabs as tab}
          <button
            class={`border rounded-full px-4 py-2.5 font-extrabold ${activeFilter === tab.value ? "bg-gray-200 text-black border-ink" : "border-[#cbded6] text-muted bg-transparent"}`}
            on:click={() => (activeFilter = tab.value)}
          >
            {tab.label}
          </button>
        {/each}
      </div>
      <div
        class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-2 xl:grid-cols-3 gap-8"
      >
        {#each visibleCars as car}
          <article
            class="bg-white rounded-3xl overflow-hidden border border-line shadow-[0_8px_24px_rgba(8,31,42,.05)] transition duration-300 hover:-translate-y-1.5 hover:shadow-brand"
          >
            <div
              class="h-[230px] bg-gradient-to-br from-[#153f4c] to-[#0c766e] grid place-items-center text-white text-8xl relative"
            >
              <span
                class="absolute top-4 left-4 bg-white text-gray-600 rounded-full px-3 py-2 text-sm font-extrabold"
                >{car.badge}</span
              >
              {car.emoji}
            </div>
            <div class="p-8">
              <h3 class="text-2xl font-display">{car.title}</h3>
              <p class="text-muted text-base mt-3">{car.desc}</p>
              <div class="flex gap-2 flex-wrap my-4">
                {#each car.meta as m}
                  <span
                    class="bg-[#f0f6f3] text-[#4d6c6d] rounded-lg px-3 py-2 text-sm font-bold"
                    >{m}</span
                  >
                {/each}
              </div>
              <div
                class="border-t border-line pt-5 mt-5 flex justify-between items-end"
              >
                <div>
                  <small class="block text-muted text-xs"
                    >{car.priceLabel}</small
                  >
                  <strong class="font-display text-3xl">{car.price}</strong>
                </div>
                <a href="#quote" class="font-extrabold text-teal text-lg"
                  >Book →</a
                >
              </div>
            </div>
          </article>
        {/each}
      </div>
    </div>
  </section>

  <!-- Self-drive -->
  <section class="bg-ink text-white py-16 md:py-24" id="self-drive">
    <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
      <div
        class="flex flex-col md:flex-row md:justify-between md:items-end gap-7 mb-9"
      >
        <div>
          <!-- <div
            class="text-xs font-extrabold tracking-[.14em] uppercase text-[#a7f1d0]"
          >
            Self-drive rentals
          </div> -->
          <h2
            class="font-display tracking-[-.045em] text-[clamp(2rem,4.5vw,3.65rem)] text-black leading-tight mt-2"
          >
            Private, flexible and ready when you are.
          </h2>
        </div>
        <p class="max-w-[500px] text-black">
           Cars are available from Pune for verified customers. Submit
          your route and dates so our team can confirm vehicle availability,
          documents and the best fare.
        </p>
      </div>
      <div
        class="grid grid-cols-1 lg:grid-cols-[1.05fr_.95fr] gap-7 items-start"
      >
        <div class="bg-[#143946] border border-gray-200 rounded-[26px] p-7">
          <h3 class="text-xl font-display">How booking works</h3>
          <div class="grid gap-3.5 mt-6">
            {#each checklist as item}
              <div class="grid grid-cols-[42px_1fr] gap-3 items-start">
                <i
                  class="w-[42px] h-[42px] rounded-2xl bg-[#a7f1d0]/[.14] grid place-items-center not-italic text-[#a7f1d0] font-extrabold"
                  >{item.n}</i
                >
                <div>
                  <b>{item.title}</b>
                  <p class="mt-1 text-white/60 text-sm">{item.text}</p>
                </div>
              </div>
            {/each}
          </div>
        </div>

        <form
          id="quote"
          class="bg-white text-black rounded-[26px] p-7 scroll-mt-24 border"
          on:submit={handleQuoteSubmit}
        >
          <div
            class="text-xs font-extrabold tracking-[.14em] uppercase text-teal"
          >
            Quick quote
          </div>
          <h3 class="text-2xl font-display mt-1.5">Request car availability</h3>

          {#if !submitted}
            <div class="grid gap-3 mt-4.5">
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-2.5">
                <label
                  class="text-xs font-extrabold uppercase tracking-wide text-muted"
                  >Your name
                  <input
                    required
                    bind:value={quoteName}
                    placeholder="Full name"
                    class="w-full mt-1.5 border border-line rounded-xl p-3.5 bg-white text-ink font-normal normal-case tracking-normal"
                  />
                </label>
                <label
                  class="text-xs font-extrabold uppercase tracking-wide text-muted"
                  >Mobile number
                  <input
                    required
                    bind:value={quotePhone}
                    placeholder="72182 83271"
                    class="w-full mt-1.5 border border-line rounded-xl p-3.5 bg-white text-ink font-normal normal-case tracking-normal"
                  />
                </label>
              </div>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-2.5">
                <label
                  class="text-xs font-extrabold uppercase tracking-wide text-muted"
                  >Rental type
                  <select
                    bind:value={quoteType}
                    class="w-full mt-1.5 border border-line rounded-xl p-3.5 bg-white text-ink font-normal normal-case tracking-normal"
                  >
                    <!-- <option>Self-drive car</option> -->
                    <option>Car with driver</option>
                    <option>Airport transfer</option>
                    <option>Monthly rental</option>
                  </select>
                </label>
                <label
                  class="text-xs font-extrabold uppercase tracking-wide text-muted"
                  >Car category
                  <select
                    bind:value={quoteCar}
                    class="w-full mt-1.5 border border-line rounded-xl p-3.5 bg-white text-ink font-normal normal-case tracking-normal"
                  >
                    <option>Hatchback</option>
                    <option>Sedan</option>
                    <option>SUV / MUV</option>
                    <option>Tempo Traveller</option>
                    <option>Premium</option>
                  </select>
                </label>
              </div>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-2.5">
                <label
                  class="text-xs font-extrabold uppercase tracking-wide text-muted"
                  >Pickup date
                  <input
                    required
                    type="date"
                    min={today}
                    bind:value={quoteDate}
                    class="w-full mt-1.5 border border-line rounded-xl p-3.5 bg-white text-ink font-normal normal-case tracking-normal"
                  />
                </label>
                <label
                  class="text-xs font-extrabold uppercase tracking-wide text-muted"
                  >Return date
                  <input
                    type="date"
                    min={today}
                    bind:value={quoteReturnDate}
                    class="w-full mt-1.5 border border-line rounded-xl p-3.5 bg-white text-ink font-normal normal-case tracking-normal"
                  />
                </label>
              </div>
              <label
                class="text-xs font-extrabold uppercase tracking-wide text-muted"
                >Route / usage
                <textarea
                  rows="3"
                  bind:value={quoteRoute}
                  placeholder="Example: Pune to Goa for 3 days, or Pune local with driver for 8 hours"
                  class="w-full mt-1.5 border border-line rounded-xl p-3.5 bg-white text-ink font-normal normal-case tracking-normal"
                ></textarea>
              </label>
              <button
                type="submit"
                class="border-1 rounded-full px-5 py-3 font-extrabold inline-flex items-center justify-center gap-2 transition hover:-translate-y-0.5 bg-orange-300 text-teal shadow-[0_12px_25px_rgba(240,100,59,.25)]"
                >Send booking request →</button
              >
              <div class="text-xs text-muted text-center">
                For faster booking, call 72182 83271 / +91 9146634563 or WhatsApp
                your route details.
              </div>
            </div>
          {:else}
            <div class="text-center py-7">
              <div
                class="w-[58px] h-[58px] rounded-full bg-mint text-teal grid place-items-center mx-auto text-2xl font-extrabold"
              >
                ✓
              </div>
              <h3 class="text-xl font-display mt-3.5">Request noted</h3>
              <p class="text-muted">
                Please call or WhatsApp us for immediate confirmation: 72182
                83271 / +91 9146634563.
              </p>
            </div>
          {/if}
        </form>
      </div>
    </div>
  </section>

  <!-- Routes -->
  <section id="routes" class="py-16 md:py-24">
    <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
      <div
        class="flex flex-col md:flex-row md:justify-between md:items-end gap-7 mb-9"
      >
        <div>
          <div
            class="text-xs font-extrabold tracking-[.14em] uppercase text-teal"
          >
            Popular routes
          </div>
          <h2
            class="font-display tracking-[-.045em] text-[clamp(2rem,4.5vw,3.65rem)] leading-tight mt-2"
          >
            Pune rentals for Maharashtra and all India.
          </h2>
        </div>
        <p class="max-w-[500px] text-muted">
          Use these as examples. We can quote local, round-trip, one-way,
          multi-city and long-duration rental plans depending on availability.
        </p>
      </div>
    <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6">
  {#each routeGroups as group}
    <article
      class="bg-white rounded-3xl p-6 border border-line shadow-sm hover:shadow-lg transition-all duration-300"
    >
      <div class="flex items-center gap-2 mb-5">
        <div
          class="w-10 h-10 rounded-full bg-primary/10 text-primary flex items-center justify-center text-lg"
        >
          📍
        </div>

        <h3 class="text-xl font-display font-bold text-[#1f3c40]">
          {group.state}
        </h3>
      </div>

      <div class="flex flex-wrap gap-2">
        {#each group.routes as route}
          <span
            class="px-4 py-2 rounded-full bg-[#f2f8f5] border border-line text-[#36595d] font-semibold text-sm hover:bg-green-500 hover:text-white transition-colors cursor-default"
          >
            {route}
          </span>
        {/each}
      </div>
    </article>
  {/each}
</div> 
    </div>
  </section>

  <!-- Process -->
  <section class="bg-ink py-16 md:py-24" id="process">
    <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
      <div
        class="flex flex-col md:flex-row md:justify-between md:items-end gap-7 mb-9"
      >
        <div>
          <div
            class="text-xs font-extrabold tracking-[.14em] uppercase text-teal"
          >
            Simple booking flow
          </div>
          <h2
            class="font-display tracking-[-.045em] text-[clamp(2rem,4.5vw,3.65rem)] leading-tight mt-2"
          >
            From enquiry to keys in four steps.
          </h2>
        </div>
        <p class="max-w-[500px] text-muted">
          Rental customers want clarity before they pay. This section keeps the
          process visible: vehicle availability, fare, documents and handover.
        </p>
      </div>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 ">
        {#each steps as step}
          <article class="bg-cream border border-line rounded-[22px] p-6 hover:bg-teal-50 transition duration-200 group-hover:scale-510 shadow-lg">
            <div
              class="w-[42px] h-[42px] rounded-full bg-ink text-black grid place-items-center font-extrabold mb-4.5"
            >
              {step.n}
            </div>
            <h3 class="text-xl text-teal font-display ">{step.title}</h3>
            <p class="text-muted text-sm mt-2">{step.text}</p>
          </article>
        {/each}
      </div>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-5 mt-6">
        <!-- <div class="bg-white border border-line rounded-[22px] p-6">
          <h3 class="text-xl font-display">Self-drive documents</h3>
          <ul class="mt-4 pl-5 text-[#49666a] leading-loose list-disc">
            {#each docsList as d}<li>{d}</li>{/each}
          </ul>
        </div> -->
        <div class="bg-white border border-line rounded-[22px] p-6">
          <h3 class="text-xl font-display">Fare clarity before booking</h3>
          <ul class="mt-4 pl-5 text-[#49666a] leading-loose list-disc">
            {#each fareList as f}<li>{f}</li>{/each}
          </ul>
        </div>
      </div>
    </div>
  </section>

  <!-- Why -->
  <section id="why" class="py-16 md:py-24 ">
    <div
      class="w-[min(1180px,calc(100%-40px))] mx-auto grid grid-cols-1 lg:grid-cols-[.9fr_1.1fr] gap-10 lg:gap-[70px] items-center"
    >
      <div
        class="bg-gray-500 text-white rounded-[34px] p-10 relative overflow-hidden"
      >
        <div
          class="absolute w-[230px] h-[230px] bg-orange rounded-full -right-32 -bottom-32"
        ></div>
        <div
          class="relative text-xs font-extrabold tracking-[.14em] uppercase text-[#a7f1d0]"
        >
          The Shree Ram promise
        </div>
        <div
          class="relative font-display text-5xl md:text-6xl font-extrabold mt-2"
        >
          Clear fare
        </div>
        <p class="relative text-white/70 mt-3">
          No confusing package pricing. We focus on car rental needs: vehicle,
          route, dates, driver choice and final fare before
          confirmation.
        </p>
        <p class="relative text-white/70 mt-4">
          <span class="text-[#ffc65b] tracking-wide">★★★★★</span><br />Built for
          Pune local, outstation customers.
        </p>
      </div>
      <div>
        <div
          class="text-xs font-extrabold tracking-[.14em] uppercase text-teal"
        >
          Why customers choose us
        </div>
        <h2
          class="font-display tracking-[-.045em] text-[clamp(2rem,4.5vw,3.65rem)] leading-tight mt-2"
        >
          Practical rental support, not just a booking form.
        </h2>
        <div class="grid gap-6 mt-8 p-5 bg-gray-200 border rounded-3xl">
          {#each whyItems as item}
            <div class="grid grid-cols-[48px_1fr] gap-4">
              <div
                class="w-12 h-12 rounded-2xl bg-mint grid place-items-center text-xl"
              >
                {item.icon}
              </div>
              <div>
                <h3 class="text-xl font-display">{item.title}</h3>
                <p class="mt-1.5 text-muted text-sm">{item.text}</p>
              </div>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </section>

  <!-- Reviews -->
  <section class="bg-[#eef7f3] py-16 md:py-24" id="reviews">
    <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
      <div class="mb-9">
        <div
          class="text-xs font-extrabold tracking-[.14em] uppercase text-teal"
        >
          Customer feedback
        </div>
        <h2
          class="font-display tracking-[-.045em] text-[clamp(2rem,4.5vw,3.65rem)] leading-tight mt-2"
        >
          Made for daily, family and business travel.
        </h2>
      </div>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4.5">
        {#each reviews as r}
          <article class="bg-white border border-line rounded-[22px] p-6 m-6 ">
            <span class="text-[#ffc65b] tracking-wide">★★★★★</span>
            <p class="text-[#38565a] mt-2">{r.text}</p>
            <div class="flex gap-3 items-center mt-5">
              <div
                class="w-[42px] h-[42px] rounded-full bg-mint grid place-items-center font-extrabold"
              >
                {r.initials}
              </div>
              <div>
                <b>{r.name}</b><br />
                <small class="text-muted">{r.tag}</small>
              </div>
            </div>
          </article>
        {/each}
      </div>
    </div>
  </section>

  <!-- FAQ -->
  <section id="faq" class="py-16 md:py-24">
    <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
      <div
        class="flex flex-col md:flex-row md:justify-between md:items-end gap-7 mb-9"
      >
        <div>
          <div
            class="text-xs font-extrabold tracking-[.14em] uppercase text-teal"
          >
            Questions before booking
          </div>
          <h2
            class="font-display tracking-[-.045em] text-[clamp(2rem,4.5vw,3.65rem)] leading-tight mt-2"
          >
            Quick answers for rental customers.
          </h2>
        </div>
        <p class="max-w-[500px] text-muted">
          These FAQs reduce phone back-and-forth and make the site feel more
          trustworthy for first-time customers.
        </p>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        {#each faqs as item}
          <article class="bg-white border border-line rounded-[20px] p-6">
            <h3 class="text-xl font-display">{item.q}</h3>
            <p class="mt-2.5 text-muted text-sm">{item.a}</p>
          </article>
        {/each}
      </div>
    </div>
  </section>
</main>

<!-- Footer -->
<footer class="bg-gray-600 text-white pt-16 pb-7">
  <div class="w-[min(1180px,calc(100%-40px))] mx-auto">
    <div
      class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-[1.5fr_1fr_1fr_1fr] gap-10"
    >
      <div>
        <a
          href="#"
          class="font-display font-extrabold text-xl flex items-center gap-2.5"
        >
          <span
            class="w-10 h-10 rounded-full grid place-items-center bg-orange text-white text-sm font-sans"
            >श्री</span
          >
          Shree Ram Travels
        </a>
        <p class="text-white/60 max-w-[340px] mt-4">
          Car rentals services based in Pune, Maharashtra,
          serving routes across India.
        </p>
        <p class="text-sm text-white/60 mt-2">Office: Pune, Maharashtra</p>
      </div>
      <div>
        <h4 class="font-display mb-4">Services</h4>
        <!-- <a href="#self-drive" class="block text-white/70 my-2.5 text-sm"
          >Self-drive cars</a
        > -->
        <a href="#fleet" class="block text-white/70 my-2.5 text-sm"
          >Car with driver</a
        >
        <a href="#services" class="block text-white/70 my-2.5 text-sm"
          >Airport transfers</a
        >
        <a href="#services" class="block text-white/70 my-2.5 text-sm"
          >Monthly rentals</a
        >
      </div>
      <div>
        <h4 class="font-display mb-4">Popular routes</h4>
        <a href="#routes" class="block text-white/70 my-2.5 text-sm"
          >Pune to Mumbai</a
        >
        <a href="#routes" class="block text-white/70 my-2.5 text-sm"
          >Pune to Goa</a
        >
        <a href="#routes" class="block text-white/70 my-2.5 text-sm"
          >Pune to Shirdi</a
        >
        <a href="#routes" class="block text-white/70 my-2.5 text-sm"
          >All India rentals</a
        >
      </div>
      <div>
        <h4 class="font-display mb-4">Contact</h4>
        <a href="tel:+917218283271" class="block text-white/70 my-2.5 text-sm"
          >+91 72182 83271</a
        >
        <a href="tel:+917219882073" class="block text-white/70 my-2.5 text-sm"
          >+91 9146634563</a
        >
        <a href="mailto:contact@shreramtravel.com">
          contact@shreramtravel.com
        </a>

        <a href="mailto:shreramtravels@gmail.com"> shreramtravels@gmail.com </a>
        <a
          href={waLink}
          target="_blank"
          rel="noopener"
          class="block text-white/70 my-2.5 text-sm">WhatsApp booking</a
        >
      </div>
    </div>
    <div
      class="border-t border-white/10 mt-12 pt-5 flex flex-col sm:flex-row justify-between gap-4 text-white/45 text-sm"
    >
      <span>© 2026 Shree Ram Travels, Pune.</span>
      <span
        >Clean cars · Chauffeur-driven rentals · All-India outstation
        service</span
      >
    </div>
  </div>
</footer>

<!-- Floating WhatsApp button -->
<!-- <a
  href={waLink}
  target="_blank"
  rel="noopener"
  aria-label="Chat with Shree Ram Travels on WhatsApp"
  class="fixed right-5 bottom-5 z-40 w-14 h-14 rounded-full bg-[#25d366] text-white grid place-items-center text-2xl shadow-[0_12px_28px_rgba(0,0,0,.22)]"
>
  ☎
</a> -->
<div class="fixed right-5 bottom-5 z-50 flex flex-col items-end gap-3">

  {#if fabOpen}
    <!-- Call Button -->
    <a
      href={`tel:${phoneNumber}`}
      class="flex items-center gap-3 bg-white rounded-full px-4 py-3 shadow-xl hover:scale-105 transition-all"
    >
      <span class="grid place-items-center w-11 h-11 rounded-full bg-blue-600 text-white text-xl">
        📞
      </span>
      <span class="font-semibold text-gray-700">Call Us</span>
    </a>

    <!-- WhatsApp Button -->
    <a
      href={waLink1}
      target="_blank"
      rel="noopener"
      class="flex items-center gap-3 bg-white rounded-full px-4 py-3 shadow-xl hover:scale-105 transition-all"
    >
      <span class="grid place-items-center w-11 h-11 rounded-full bg-[#25D366] text-white text-xl">
        💬
      </span>
      <span class="font-semibold text-gray-700">WhatsApp</span>
    </a>
  {/if}

  <!-- Main Floating Button -->
  <button
    on:click={() => (fabOpen = !fabOpen)}
    class="w-16 h-16 rounded-full bg-primary text-white shadow-2xl text-3xl hover:scale-110 transition-all"
    aria-label="Contact Options"
  >
    {#if fabOpen}
      ✕
    {:else}
      ☎
    {/if}
  </button>

</div>