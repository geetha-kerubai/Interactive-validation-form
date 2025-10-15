# Interactive-validation-form
 
<!DOCTYPE html> 
<html lang="en"> 
<head> 
<meta charset="UTF-8" /> 
<meta name="viewport" content="width=device-width, initial-scale=1.0" /> 
<title>Interactive Multi-Page Form</title> 
<style> 
:root{ 
  --accent:#bf00ff; 
  --accent-light:#ff33cc; 
  --danger:#e74c3c; 
  --bg:#f6f8fb; 
  --card:#fff; 
  --radius:12px; 
  --shadow:0 6px 20px rgba(0,0,0,0.1); 
} 
 
body{   background:linear-gradient(135deg,var(--accent),var(--accent-light));   font-family:"Poppins",sans-serif; 
  display:flex;   justify-content:center;   align-items:center;   height:100vh;   margin:0; 
} 
 
.container{   width:90%;   max-width:400px; 
} 
 
.page{   background:var(--card);   border-radius:var(--radius);   box-shadow:var(--shadow);   padding:2rem;   display:none; 
  animation:fadeIn 0.5s ease; 
} 
 
.page.active{   display:block; 
} 
 
h2{ 
text-align:center; 
color:var(--accent); 
} 
 
.input-group{   display:flex;   flex-direction:column;   margin-bottom:1rem; 
} 
 
label{   font-size:0.9rem;   margin-bottom:0.3rem;   color:#333; 
} 
 
input{   padding:0.7rem;   border:1px solid #ccc;   border-radius:8px;   font-size:1rem;   outline:none; 
} 
 
input:focus{   border-color:var(--accent); 
  box-shadow:0 0 6px rgba(191,0,255,0.3); 
} 
 
.error{   color:var(--danger);   font-size:0.8rem;   height:14px; 
} 
 
button{   background:linear-gradient(90deg,var(--accent),var(--accent-light));   color:#fff;   border:none;   border-radius:8px;   padding:0.8rem;   width:100%;   font-weight:600;   cursor:pointer;   transition:all 0.3s; 
} 
 
button:hover{   opacity:0.9; 
  transform:translateY(-1px); 
}
.switch{   text-align:center;   margin-top:1rem;   font-size:0.9rem; 
} 
 
.switch span{   color:var(--accent);   cursor:pointer;   font-weight:600; 
} 
 
.success{   text-align:center;   font-size:1.2rem;   color:var(--accent); 
} 
 
@keyframes fadeIn{   from{opacity:0;transform:translateY(20px);}   to{opacity:1;transform:translateY(0);} 
} 
 
/* Mobile responsive */ 
@media (max-width:480px){   .page{padding:1.5rem;}   h2{font-size:1.5rem;} 
} 
</style> 
</head> 
<body> 
 
<div class="container"> 
 
  <!-- PAGE 1: LOGIN --> 
  <div id="loginPage" class="page active"> 
    <h2>Login</h2> 
    <div class="input-group"> 
      <label>Email</label> 
      <input type="email" id="loginEmail" placeholder="Enter your email" required />       <small class="error"></small> 
    </div> 
    <div class="input-group"> 
      <label>Password</label> 
      <input type="password" id="loginPassword" placeholder="Enter password" required minlength="6"/> 
      <small class="error"></small> 
   </div> 
  <button id="loginBtn">Login</button> 
  <p class="switch">Don't have an account? <span id="createAccount">Create one</span></p> 
  </div> 
 
  <!-- PAGE 2: CREATE ACCOUNT --> 
  <div id="signupPage" class="page"> 
    <h2>Create Account</h2> 
    <div class="input-group"> 
      <label>Full Name</label> 
      <input type="text" id="signupName" placeholder="Enter your name" required />       <small class="error"></small> 
    </div> 
    <div class="input-group"> 
      <label>Email</label> 
      <input type="email" id="signupEmail" placeholder="Enter your email" required />       <small class="error"></small> 
    </div> 
    <div class="input-group"> 
      <label>Password</label> 
      <input type="password" id="signupPassword" placeholder="Enter password" required minlength="6"/> 
      <small class="error"></small> 
    </div> 
    <button id="signupBtn">Create Account</button> 
    <p class="switch">Already have an account? <span id="goLogin">Login</span></p>   </div> 
 
  <!-- PAGE 3: MAIN FORM --> 
  <div id="mainFormPage" class="page"> 
    <h2>Personal Details</h2> 
 
    <div class="input-group"> 
      <label>Person Name</label> 
      <input type="text" id="personName" placeholder="Enter person name" required />       <small class="error"></small> 
    </div> 
 
    <div class="input-group"> 
      <label>Date of Birth</label> 
      <input type="date" id="dob" required /> 
      <small class="error"></small> 
    </div> 
 
    <div class="input-group"> 
      <label>Phone Number</label> 
      <input type="text" id="phone" placeholder="Enter your number" required pattern="[09]{10}"/> 
      <small class="error"></small> 
   </div> 
  <div class="input-group"> 
      <label>Address</label> 
      <input type="text" id="address" placeholder="Enter your address" required /> 
      <small class="error"></small> 
    </div> 
 
    <button id="submitForm">Submit</button> 
  </div> 
 
  <!-- PAGE 4: SUCCESS --> 
  <div id="successPage" class="page">     <h2>  Registered Successfully!</h2> 
    <p class="success">Thank you for completing the registration process.</p> 
  </div> 
</div> 
 
<script> const loginPage = document.getElementById('loginPage'); const signupPage = document.getElementById('signupPage'); const mainFormPage = document.getElementById('mainFormPage'); const successPage = document.getElementById('successPage'); 
 
const loginBtn = document.getElementById('loginBtn'); const signupBtn = document.getElementById('signupBtn'); const submitForm = document.getElementById('submitForm'); 
 
const createAccount = document.getElementById('createAccount'); const goLogin = document.getElementById('goLogin'); 
 
// Switch pages createAccount.onclick = () => {   loginPage.classList.remove('active');   signupPage.classList.add('active'); 
}; 
 
goLogin.onclick = () => {   signupPage.classList.remove('active');   loginPage.classList.add('active'); 
}; 
 
// Simple error helpers function showError(input, msg){   const small = input.parentElement.querySelector('.error');   small.textContent = msg;   input.style.borderColor = 'var(--danger)'; 
} 
 
function clearError(input){ 
 const small = input.parentElement.querySelector('.error');  small.textContent = ''; 
input.style.borderColor = '#ccc'; 
} 
 
// LOGIN validation loginBtn.onclick = () => {   const email = document.getElementById('loginEmail'); 
  const pass = document.getElementById('loginPassword');   let valid = true; 
 
  if(email.value.trim()===''){showError(email,'Email required');valid=false;} else clearError(email);   if(pass.value.length<6){showError(pass,'Min 6 characters');valid=false;} else clearError(pass); 
 
  if(valid){     loginPage.classList.remove('active'); 
    mainFormPage.classList.add('active'); 
  } 
}; 
 
// SIGNUP validation signupBtn.onclick = () => {   const name = document.getElementById('signupName');   const email = document.getElementById('signupEmail'); 
  const pass = document.getElementById('signupPassword');   let valid = true; 
 
  if(name.value.trim()===''){showError(name,'Name required');valid=false;} else clearError(name);   if(email.value.trim()===''){showError(email,'Email required');valid=false;} else clearError(email);   if(pass.value.length<6){showError(pass,'Min 6 characters');valid=false;} else clearError(pass); 
 
  if(valid){     signupPage.classList.remove('active'); 
    mainFormPage.classList.add('active'); 
  } 
}; 
 
// MAIN FORM validation (with person name + DOB) 
submitForm.onclick = () => {   const personName = document.getElementById('personName');   const dob = document.getElementById('dob');   const phone = document.getElementById('phone');   const address = document.getElementById('address');   let valid = true; 
 
  if(personName.value.trim()===''){showError(personName,'Person name required');valid=false;} else clearError(personName); if(dob.value===''){showError(dob,'Please select date of birth');valid=false;} else 
clearError(dob);   if(!/^[0-9]{10}$/.test(phone.value)){showError(phone,'Enter valid 10-digit number');valid=false;} else clearError(phone);   if(address.value.trim()===''){showError(address,'Address required');valid=false;} else clearError(address); 
 
  if(valid){ 
    mainFormPage.classList.remove('active'); 
    successPage.classList.add('active'); 
  } 
}; 
</script> 
 
</body> 
</html> 
