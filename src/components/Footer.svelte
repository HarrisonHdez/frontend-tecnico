<script>
  let title = 'Our Mission';
  let paragraph = 'At TaskMaster, we are dedicated to helping you stay organized, focused, and achieve your goals. We provide a user-friendly platform to manage your tasks effectively, prioritize your work, and make progress towards your objectives. Let us be your companion on your journey to success.';
    let icon = './svg/github.svg';
    let currentYear = new Date().getFullYear();
</script>

<footer class="footer" aria-label="Pie de página">
  <div class="footer__content container">
    <h4 class="footer__title">{title}</h4>
    <div class="footer__paragraph-container">
        <p class="footer__paragraph">{paragraph}</p>
        <img class="footer__icon" src={icon} alt="GitHub Icon"/>
    </div>
    <p class="footer__full-year">© {currentYear}  Fernando Leano. All rights reserved.</p>
  </div>
</footer>

<style>
.footer {
    width: 100%;
    min-height: 204px;
    height: auto;
    background-color: var(--primary-color);

}
.footer__content {
    padding: 24px;
    min-height: 204px;
    height: auto;
    text-align: center;
}

.footer__title {
    text-align: center;
    color: white;
    margin-bottom: 12px;
    font-size: 18px;
    font-family: 'Lato', sans-serif;
    font-weight: 700;
}
.footer__icon {
    margin-top: 35px;
}
.footer__paragraph {
    font-family: 'Lato', sans-serif;
    font-weight: 400;
    font-size: 14px;
    line-height: 20px;
    color: var(--paragraph-color);
    margin-bottom: 16px;
}
.footer__full-year {
    font-family: 'Lato', sans-serif;
    font-weight: 400;
    font-size: 16px;
    color: var(--paragraph-color);
    margin: 24px 0 16px
}

@media screen and (min-width: 768px) {
   .footer__paragraph-container {
        display: flex;
    }
    .footer__icon {
    margin: 0;
    }
    .footer__paragraph {
        margin-right: 5px;
    }
} 
</style>
