<template>
  <div class="homepage">
    <!-- Hero Section with Background Image -->
    <div class="hero-section">
      <div class="content">
        <img src="./logo.png" alt="" class="headSection">
        <h1 class="title">Welcome to Our DivySparsh Jewellers</h1>
        <p class="subtitle">Find the perfect piece for you or sell your jewelry with ease.</p>

        <div class="buttons">
          <button @click="openSellForm" class="btn sell-btn">Sell Jewelry</button>
          <button @click="openBuyForm" class="btn buy-btn">Buy Jewelry</button>
        </div>
      </div>
    </div>

    <!-- Sell Form Modal -->
    <div v-if="showSellForm" class="modal">
      <div class="modal-content">
        <h2 style="color: green;">Sell Your Jewelry</h2>
        <form @submit.prevent="generateSellPDF" class="form sell-form">
          <div class="form-group">
            <label for="buyerName">Your Name:</label>
            <input type="text" v-model="buyerName" id="buyerName" required>
          </div>
          <div class="form-group">
            <label for="buyerMobile">Your Mobile:</label>
            <input type="number" v-model="buyerMobile" id="buyerMobile" required>
          </div>
          <div class="form-group">
            <label for="purchasedItem">Jewellery Item:</label>
            <input type="text" v-model="purchasedItem" id="purchasedItem" required>
          </div>
          <div class="form-group">
            <label for="amount">Total Amount:</label>
            <input type="number" v-model="amount" id="amount" required>
          </div>
          <div class="form-group">
            <label for="weight">Weight:</label>
            <input type="text" v-model="weight" id="weight" required>
          </div>
       
          <div class="form-buttons">
            <button type="button" @click="closeSellForm" class="btn close-btn">Close</button>
            <button type="submit" class="btn submit-btn">Submit & Generate PDF</button>
          </div>
        </form>
      </div>
    </div>

    <!-- Buy Form Modal -->
    <div v-if="showBuyForm" class="modal" @submit.prevent="generateSellPDF">
      <div class="modal-content">
        <h2 style="color: red;">Buy Jewelry</h2>
        <form @submit.prevent="handleBuy" class="form buy-form">
          <div class="form-group">
            <label for="buyerName">Your Name:</label>
            <input type="text" v-model="buyerName" id="buyerName" required>
          </div>
          <div class="form-group">
            <label for="buyerMobile">Your Mobile:</label>
            <input type="number" v-model="buyerMobile" id="buyerMobile" required>
          </div>
          <div class="form-group">
            <label for="itemOfInterest">Item (Jewellery):</label>
            <input type="text" v-model="purchasedItem" id="itemOfInterest" required>
          </div>
          <div class="form-group">
            <label for="budget">Weight:</label>
            <input type="text" v-model="weight" id="budget" required>
          </div>
          <div class="form-group">
            <label for="budget">Amount:</label>
            <input type="number" v-model="amount" id="budget" required>
          </div>
          <div class="form-buttons">
            <button type="button" @click="closeBuyForm" class="btn close-btn">Close</button>
            <button type="submit" class="btn submit-btn">Submit & Generate PDF</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import html2pdf from "html2pdf.js";

export default {
  data() {
    return {
      showSellForm: false,
      showBuyForm: false,

      // Sell Form Data
      buyerName: "",
      buyerMobile: "",
      purchasedItem: "",
      amount: 0,
      weight: "",
      date: new Date().toISOString().substr(0, 10), // Default to today's date

      // Buy Form Data
      itemOfInterest: "",
      budget: 0,
    };
  },
  computed: {
    currentDate() {
      return new Date().toISOString().substr(0, 10); // Format for date input
    }
  },
  methods: {
    openSellForm() {
      this.showSellForm = true;
    },
    closeSellForm() {
      this.showSellForm = false;
    },
    generateSellPDF() {
  // Format table data as plain text with bold text
  const message = `
*श्री गणेशाय नमः*

*DivySparsh Jewellers*
Address: Gurwaliya Bazaar, Sabji Mandi Gali ke Samne, Spaha-Turpatti Road Kushinagar U.P. 274407

*Customer Details:*
• *Name:* ${this.buyerName}
• *Mobile:* ${this.buyerMobile}

*Item Details:*
• *Jewellery Item:* ${this.purchasedItem}
• *Total Amount:* ₹ ${this.amount}
• *Weight:* ${this.weight}
• *Date:* ${this.date}

*Authorized Signatory:*
• Vipin Verma
• 9067324496

 आपका दिन मंगलमय हो | कृपया पुनः पधारे
`;

  // Encode the message
  const encodedMessage = encodeURIComponent(message);

  // Replace with the recipient's phone number in international format
  const phoneNumber = this.buyerMobile; 

  // Create WhatsApp URL
  const whatsappUrl = `https://wa.me/${phoneNumber}?text=${encodedMessage}`;

  // Open WhatsApp Web in a new tab or window
  window.open(whatsappUrl, '_blank');

  // Optionally, close the form and alert the user
  // this.closeSellForm();
  // alert("Message sent via WhatsApp!");
}
,
    openBuyForm() {
      this.showBuyForm = true;
    },
    cleardata(){
      this.buyerName = "";
      this.buyerMobile = "";
      this.amount = "";
      this.weight = "";
      this.purchasedItem=''

    },
    closeBuyForm() {
      this.showBuyForm = false;
    },
    handleBuy() {
      // Handle buy form submission
      // alert("Buy form submitted!");
      this.closeBuyForm();
    },
  },
};
</script>

<style scoped>
.homepage {
  width: 100vw;
  height: 100vh;
}

/* Hero Section */
.hero-section {
  background-image: url('https://5.imimg.com/data5/SELLER/Default/2022/3/VY/MT/NA/14579595/jewellery-and-gems-website-design-development-services-hyderabad.jpg');
  background-size: cover;
  background-position: center;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  text-align: center;
  color: red;
  padding: 20px;
}

.headSection {
  width: 500px;
  height: auto;
}

.title {
  font-size: 2.5rem;
  margin: 1rem;
}

.subtitle {
  font-size: 1.2rem;
  margin: 1.9rem 0px;
}
.buttons{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.buttons .btn {
  font-size: 1.7rem;
  padding: 8px 16px;
  margin:20px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
}

.sell-btn {
  background-color: green;
  color: white;
}

.buy-btn {
  background-color: #3498db;
  color: white;
}

.btn:hover {
  background-color: #000;
}

/* Modal Styles */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  text-align: left;
  background: white;
  padding: 20px;
  border-radius: 8px;
  width: 90%;
  max-width: 500px;
  height: 80vh;
  overflow-y: auto;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  animation: fadeIn 0.3s ease-in-out;
}

.modal-content h2 {
  margin-bottom: 20px;
  font-size: 1.5rem;
}

.form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 1rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: bold;
}

.form-group input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  outline: none;
}

.form-group input:focus {
  outline: 2px solid pink;
}

.form-buttons {
  display: flex;
  justify-content: space-between;
  margin-top: 1rem;
}

.btn {
  border: none;
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  cursor: pointer;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.submit-btn {
  background-color: #4caf50;
  color: white;
}

.submit-btn:hover {
  background-color: #45a049;
}

.close-btn {
  background-color: #f44336;
  color: white;
}

.close-btn:hover {
  background-color: #e53935;
}

/* Tablet and smaller screens */
@media screen and (max-width: 768px) {
  .hero-section {
    height: auto;
    padding: 20px;
  }

  .headSection {
    width: 250px;
  }

  .title {
    font-size: 2rem;
  }

  .subtitle {
    font-size: 1rem;
  }

  /* .buttons .btn {
    font-size: 1.2rem;
    padding: 6px 12px;
    margin: 0 10px;
  } */

  .modal-content {
    width: 100%;
    max-width: 400px;
    height: auto;
  }
}

/* Mobile screens */
@media screen and (max-width: 480px) {
  .hero-section {
    height: 100vh;
    padding: 15px;
  }

  .headSection {
    width: 200px;
  }

  .title {
    font-size: 1.8rem;
  }

  .subtitle {
    font-size: 0.9rem;
  }

  /* .buttons .btn {
    font-size: 1.7rem;
    padding: 5px 10px;
    margin: 0 5px;
  } */

  .modal-content {
    width: 100%;
    max-width: 350px;
    height: auto;
  }
}

</style>
