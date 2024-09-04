<template>
    <div class="footer">
      <!-- <div class="footer-column">
        <h3>MENU</h3>
        <ul>
          <li><router-link to="/" tag="span" class="footer-link">Home</router-link></li>
          <li><router-link to="/products" tag="span" class="footer-link">Products</router-link></li>
          <li><router-link to="/about" tag="span" class="footer-link">About Us</router-link></li>
          <li><router-link to="/contact" tag="span" class="footer-link">Contact Us</router-link></li>
        </ul>
      </div> -->
      <div class="footer-column">
        <h5>For More Info :</h5>
        <p>Email: info@powertrack.com</p>
        <p>Phone: +1234567890</p>
      </div>
      <!-- <div class="footer-column">
        <h3>Follow Us</h3>
        <ul>
        <a href="#" class="icon" id="whatsapp-icon"><i class="fa-brands fa-square-whatsapp"></i></a>
        <a href="#" class="icon" id="instagram-icon"><i class="fa-brands fa-square-instagram"></i></a>
        <a href="#" class="icon" id="facebook-icon"><i class="fa-brands fa-square-facebook"></i></a>
        </ul>
      </div> -->
    </div>
  </template>
  
  <script>
  export default {
    name: 'footerComp',
  };
  </script>
  
  <style>
  .footer {
    background: #978909;;
    color: #dcdfb2;
    text-align: center;
    padding: 20px 10px;
    display: flex;
    flex-wrap: wrap;
  }
  
  .footer-column {
    flex: 1 1 100%;
    margin: 0 5px;
    margin-bottom: 20px;
  }
  
  .footer-column h3 {
    font-size: 16px;
    margin-bottom: 10px;
  }
  
  .footer-column ul {
    list-style: none;
    padding: 0;
  }
  
  .footer-column ul li {
    margin-bottom: 5px;
  }
  
  .footer-column ul li a {
    color: #dcdfb2;
    text-decoration: none;
  }
  
  .footer-column ul li a:hover {
    text-decoration: underline;
  }
  
  .footer-link {
    cursor: pointer;
    transition: color 0.3s ease;
  }
  
  .footer-link:hover {
    color: #eb4d4b;
  }
  
  .social-link {
    color: #333;
    text-decoration: none;
    margin-right: 5px;
  }
  
  .social-link:hover {
    color: #eb4d4b;
  }
  
  /* Media Queries */
  @media only screen and (min-width: 768px) {
    .footer-column {
      flex: 1;
    }
  
    .footer-column h3 {
      font-size: 18px;
    }
  }
  
  @media only screen and (min-width: 992px) {
    .footer-column {
      flex: 1;
      margin: 0 20px;
    }
  
    .footer-column h3 {
      font-size: 20px;
    }
  }
  
  </style>