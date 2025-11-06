// Campos
const form = document.getElementById("user-form");
const nameInput = document.getElementById("name");
const emailInput = document.getElementById("email");
const passwordInput = document.getElementById("password");
const confirmPasswordInput = document.getElementById("confirm-password");
const birthdateInput = document.getElementById("birthdate");
const phoneInput = document.getElementById("phone");
const termsInput = document.getElementById("terms");
const saveBtn = document.getElementById("save-btn");

// Mensagens de erro
const nameError = document.getElementById("name-error");
const emailError = document.getElementById("email-error");
const passwordError = document.getElementById("password-error");
const confirmPasswordError = document.getElementById("confirm-password-error");
const birthdateError = document.getElementById("birthdate-error");
const phoneError = document.getElementById("phone-error");
const termsError = document.getElementById("terms-error");

// Lista de usuários
const emptyState = document.getElementById("empty-state");
const userTable = document.getElementById("user-table");
const usersTbody = document.getElementById("users-tbody");
const userCountLabel = document.getElementById("user-count");

const users = [];

// Funções de validação
function setValidState(input, errorElement, message = "") {
  if (message) {
    input.classList.add("is-invalid");
    input.classList.remove("is-valid");
    errorElement.textContent = message;
  } else {
    input.classList.remove("is-invalid");
    if (input.value.trim() !== "") {
      input.classList.add("is-valid");
    } else {
      input.classList.remove("is-valid");
    }
    errorElement.textContent = "";
  }
}

function validateName() {
  const value = nameInput.value.trim();
  if (value.length === 0) {
    setValidState(nameInput, nameError, "O nome é obrigatório.");
    return false;
  }
  if (value.length < 3) {
    setValidState(nameInput, nameError, "O nome deve ter pelo menos 3 caracteres.");
    return false;
  }
  setValidState(nameInput, nameError);
  return true;
}

function validateEmail() {
  const value = emailInput.value.trim();
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (value.length === 0) {
    setValidState(emailInput, emailError, "O e-mail é obrigatório.");
    return false;
  }
  if (!emailRegex.test(value)) {
    setValidState(emailInput, emailError, "Informe um e-mail válido.");
    return false;
  }
  setValidState(emailInput, emailError);
  return true;
}

function validatePassword() {
  const value = passwordInput.value;
  if (value.length === 0) {
    setValidState(passwordInput, passwordError, "A senha é obrigatória.");
    return false;
  }
  if (value.length < 8) {
    setValidState(passwordInput, passwordError, "A senha deve ter pelo menos 8 caracteres.");
    return false;
  }
  const hasLetter = /[A-Za-z]/.test(value);
  const hasNumber = /[0-9]/.test(value);
  if (!hasLetter || !hasNumber) {
    setValidState(passwordInput, passwordError, "A senha deve conter letras e números.");
    return false;
  }
  setValidState(passwordInput, passwordError);
  return true;
}

function validateConfirmPassword() {
  const passwordValue = passwordInput.value;
  const confirmValue = confirmPasswordInput.value;
  if (confirmValue.length === 0) {
    setValidState(confirmPasswordInput, confirmPasswordError, "Confirme a senha.");
    return false;
  }
  if (passwordValue !== confirmValue) {
    setValidState(confirmPasswordInput, confirmPasswordError, "As senhas não coincidem.");
    return false;
  }
  setValidState(confirmPasswordInput, confirmPasswordError);
  return true;
}

function validateBirthdate() {
  const value = birthdateInput.value;
  if (!value) {
    setValidState(birthdateInput, birthdateError, "A data de nascimento é obrigatória.");
    return false;
  }
  setValidState(birthdateInput, birthdateError);
  return true;
}

function validatePhone() {
  const value = phoneInput.value.trim();
  if (value.length === 0) {
    // Campo opcional, então se estiver vazio é válido
    setValidState(phoneInput, phoneError);
    return true;
  }
  // Checa se tem pelo menos (99) 9999-9999 (mínimo 14 chars)
  if (value.length < 14) {
    setValidState(phoneInput, phoneError, "Informe um telefone completo ou deixe em branco.");
    return false;
  }
  setValidState(phoneInput, phoneError);
  return true;
}

function validateTerms() {
  if (!termsInput.checked) {
    termsError.textContent = "Você deve aceitar os termos.";
    return false;
  }
  termsError.textContent = "";
  return true;
}

function updateSaveButtonState() {
  const allValid =
    validateName() &&
    validateEmail() &&
    validatePassword() &&
    validateConfirmPassword() &&
    validateBirthdate() &&
    validatePhone() &&
    validateTerms();

  saveBtn.disabled = !allValid;
}

// Máscara simples de telefone
function applyPhoneMask(value) {
  const digits = value.replace(/\D/g, "").slice(0, 11); // até 11 dígitos
  const len = digits.length;

  if (len === 0) return "";
  if (len <= 2) return `(${digits}`;
  if (len <= 6) return `(${digits.slice(0, 2)}) ${digits.slice(2)}`;
  if (len <= 10) {
    // formato fixo: (xx) xxxx-xxxx
    return `(${digits.slice(0, 2)}) ${digits.slice(2, 6)}-${digits.slice(6)}`;
  }
  // formato celular: (xx) xxxxx-xxxx
  return `(${digits.slice(0, 2)}) ${digits.slice(2, 7)}-${digits.slice(7)}`;
}

function handlePhoneInput(e) {
  const formatted = applyPhoneMask(e.target.value);
  e.target.value = formatted;
  validatePhone();
  updateSaveButtonState();
}

// Eventos de validação em tempo real
nameInput.addEventListener("input", () => {
  validateName();
  updateSaveButtonState();
});

emailInput.addEventListener("input", () => {
  validateEmail();
  updateSaveButtonState();
});

passwordInput.addEventListener("input", () => {
  validatePassword();
  validateConfirmPassword();
  updateSaveButtonState();
});

confirmPasswordInput.addEventListener("input", () => {
  validateConfirmPassword();
  updateSaveButtonState();
});

birthdateInput.addEventListener("change", () => {
  validateBirthdate();
  updateSaveButtonState();
});

phoneInput.addEventListener("input", handlePhoneInput);

termsInput.addEventListener("change", () => {
  validateTerms();
  updateSaveButtonState();
});

// Submissão do formulário
form.addEventListener("submit", function (event) {
  event.preventDefault();

  // Valida tudo novamente na submissão
  const isValid =
    validateName() &&
    validateEmail() &&
    validatePassword() &&
    validateConfirmPassword() &&
    validateBirthdate() &&
    validatePhone() &&
    validateTerms();

  if (!isValid) {
    return;
  }

  const newUser = {
    name: nameInput.value.trim(),
    email: emailInput.value.trim()
  };

  users.push(newUser);
  renderUserList();

  // Limpa o formulário
  form.reset();
  [nameInput, emailInput, passwordInput, confirmPasswordInput, birthdateInput, phoneInput].forEach((input) => {
    input.classList.remove("is-valid", "is-invalid");
  });
  updateSaveButtonState();
});

function renderUserList() {
  usersTbody.innerHTML = "";
  users.forEach((user) => {
    const tr = document.createElement("tr");
    const tdName = document.createElement("td");
    const tdEmail = document.createElement("td");

    tdName.textContent = user.name;
    tdEmail.textContent = user.email;

    tr.appendChild(tdName);
    tr.appendChild(tdEmail);
    usersTbody.appendChild(tr);
  });

  userCountLabel.textContent = `${users.length} usuário(s)`;
  if (users.length > 0) {
    emptyState.style.display = "none";
    userTable.style.display = "table";
  } else {
    emptyState.style.display = "block";
    userTable.style.display = "none";
  }
}
