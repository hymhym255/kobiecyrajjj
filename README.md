<script>
  // Obsługa wybierania gwiazdek
  const stars = document.querySelectorAll('.star');
  let selectedRating = 0;

  stars.forEach(star => {
    star.addEventListener('click', () => {
      selectedRating = star.getAttribute('data-value');
      updateStars();
    });
  });

  function updateStars() {
    stars.forEach(star => {
      star.classList.toggle('active', star.getAttribute('data-value') <= selectedRating);
    });
  }

  // Funkcja dodawania opinii
  function addReview() {
    const nameInput = document.getElementById('reviewer-name');
    const textInput = document.getElementById('reviewer-text');
    const container = document.getElementById('reviews-container');

    if (!nameInput.value || !textInput.value || selectedRating === 0) {
      alert("Proszę wpisać imię, opinię i wybrać ocenę gwiazdkową!");
      return;
    }

    // Tworzenie gwiazdek tekstowych
    let starString = "";
    for(let i=0; i<5; i++) {
      starString += i < selectedRating ? "⭐" : "☆";
    }

    // Tworzenie nowej karty opinii
    const newCard = document.createElement('div');
    newCard.className = 'testimonial-card new-review';
    newCard.innerHTML = `
      <div class="stars">${starString}</div>
      <p>"${textInput.value}"</p>
      <span class="patient-name">- ${nameInput.value}</span>
    `;

    // Dodanie do kontenera
    container.prepend(newCard);

    // Resetowanie formularza
    nameInput.value = "";
    textInput.value = "";
    selectedRating = 0;
    updateStars();

    alert("Dziękujemy za dodanie opinii! Pojawiła się na liście.");
  }
</script>
