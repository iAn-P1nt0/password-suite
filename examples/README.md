# Password Utils Examples

This directory contains practical examples demonstrating all features of the `@ian-p1nt0/password-utils` library.

## Setup

### Option 1: Install from npm (Once Published)

```bash
npm install @ian-p1nt0/password-utils
```

### Option 2: Install from Local Package

From the examples directory:

```bash
npm install
```

This will install the package from the parent directory using the local tarball.

## Running the Examples

Each example can be run independently:

```bash
# Example 1: Basic Password Generation
node 1-basic-password.js

# Example 2: Passphrase Generation
node 2-passphrase.js

# Example 3: Strength Analysis
node 3-strength-analysis.js

# Example 4: Quick Validation
node 4-quick-validation.js

# Example 5: Comprehensive Demo
node 5-comprehensive-demo.js
```

Or run all examples:

```bash
npm run demo
```

---

## Examples Overview

### 1. Basic Password Generation (`1-basic-password.js`)

Demonstrates core password generation features:

- Default password generation
- Custom length passwords
- Alphanumeric-only passwords
- Excluding ambiguous characters
- PIN/number-only generation
- Maximum security passwords

**Key Features:**
- ✅ Cryptographically secure randomness
- ✅ Configurable character sets
- ✅ Entropy calculation
- ✅ Strength classification

**Example Output:**
```
Password: Kp9$mNz2@Qw5Xr8T
Strength: very-strong
Entropy: 95.20 bits
```

---

### 2. Passphrase Generation (`2-passphrase.js`)

Shows how to generate memorable Diceware passphrases:

- Default passphrases
- Different separators (dash, space, symbol, none)
- Capitalization strategies
- Adding numbers for extra security
- Pre-configured memorable passphrases

**Key Features:**
- ✅ Diceware-based word selection
- ✅ 384-word EFF subset
- ✅ Customizable formatting
- ✅ High entropy with memorability

**Example Output:**
```
Passphrase: Forest-Mountain-River-Sky-Ocean47
Strength: very-strong
Entropy: 67.20 bits
```

---

### 3. Strength Analysis (`3-strength-analysis.js`)

Comprehensive password strength analysis:

- Testing various password types
- Pattern detection
- Crack time estimation
- Actionable feedback
- Weakness identification

**Key Features:**
- ✅ zxcvbn-powered analysis
- ✅ Pattern recognition (keyboard patterns, dates, sequences)
- ✅ Detailed suggestions
- ✅ Security scoring (0-100)

**Example Output:**
```
Password: "password123"
Score: 12/100
Strength: WEAK
Crack Time: instant
⚠️  Warning: This is a top-100 common password
Suggestions:
  • Add more unique characters
  • Avoid predictable sequences
```

---

### 4. Quick Validation (`4-quick-validation.js`)

Real-time password validation for forms:

- Progressive typing simulation
- Minimum requirements checking
- Form validation examples
- Performance comparison

**Key Features:**
- ✅ Lightweight validation (no zxcvbn)
- ✅ Instant feedback
- ✅ Requirement checking
- ✅ Form integration ready

**Example Output:**
```
Password: "MyP@ssw0rd123"
🟢 Strength: STRONG (75/100)
✅ Meets minimum requirements
Feedback: Password is strong
```

---

### 5. Comprehensive Demo (`5-comprehensive-demo.js`)

Complete demonstration of all features:

- Batch password generation
- Pronounceable passwords
- Security comparisons
- Real-time validation simulation
- TOTP formatting
- Security recommendations

**Key Features:**
- ✅ All library features in one place
- ✅ Realistic use cases
- ✅ Best practices
- ✅ Performance insights

---

## API Reference

### Password Generation

```javascript
const { generatePassword } = require('@ian-p1nt0/password-utils');

// Basic usage
const result = generatePassword();

// With options
const result = generatePassword({
  length: 20,
  includeUppercase: true,
  includeLowercase: true,
  includeNumbers: true,
  includeSymbols: true,
  excludeAmbiguous: false
});
```

### Batch Generation

```javascript
const { generatePasswords } = require('@ian-p1nt0/password-utils');

const passwords = generatePasswords(10, { length: 16 });
```

### Passphrase Generation

```javascript
const { generatePassphrase } = require('@ian-p1nt0/password-utils');

const result = generatePassphrase({
  wordCount: 5,
  separator: 'dash',
  capitalization: 'first',
  includeNumber: true
});
```

### Strength Analysis

```javascript
const { analyzePasswordStrength } = require('@ian-p1nt0/password-utils');

const analysis = analyzePasswordStrength('MyPassword123!');
// Returns: { score, strength, entropy, crackTime, warning, suggestions, weaknesses }
```

### Quick Validation

```javascript
const { quickStrengthCheck, meetsMinimumRequirements } = require('@ian-p1nt0/password-utils');

const quick = quickStrengthCheck('password');
// Returns: { score, strength, feedback, weaknesses }

const requirements = meetsMinimumRequirements('password');
// Returns: { meets, missingRequirements }
```

### TOTP Formatting

```javascript
const { formatTOTPCode } = require('@ian-p1nt0/password-utils');

const formatted = formatTOTPCode('123456');
// Returns: "123 456"
```

---

## Common Use Cases

### 1. Password Manager

```javascript
const { generatePassword, analyzePasswordStrength } = require('@ian-p1nt0/password-utils');

function createNewPassword(options) {
  const password = generatePassword(options);
  const analysis = analyzePasswordStrength(password.password);

  return {
    password: password.password,
    strength: analysis.strength,
    entropy: analysis.entropy,
    crackTime: analysis.crackTime
  };
}
```

### 2. User Registration Form

```javascript
const { quickStrengthCheck, meetsMinimumRequirements } = require('@ian-p1nt0/password-utils');

function validateRegistrationPassword(password) {
  const requirements = meetsMinimumRequirements(password);

  if (!requirements.meets) {
    return {
      valid: false,
      errors: requirements.missingRequirements
    };
  }

  const check = quickStrengthCheck(password);

  if (check.score < 50) {
    return {
      valid: false,
      errors: ['Password is too weak', ...check.weaknesses]
    };
  }

  return { valid: true };
}
```

### 3. Security Dashboard

```javascript
const { analyzePasswordStrength } = require('@ian-p1nt0/password-utils');

function auditPasswordSecurity(passwords) {
  return passwords.map(pwd => {
    const analysis = analyzePasswordStrength(pwd);
    return {
      password: pwd,
      score: analysis.score,
      needsUpdate: analysis.score < 60,
      suggestions: analysis.suggestions
    };
  });
}
```

---

## TypeScript Usage

All examples can be converted to TypeScript:

```typescript
import {
  generatePassword,
  analyzePasswordStrength,
  type GeneratedPassword,
  type PasswordStrengthResult
} from '@ian-p1nt0/password-utils';

const result: GeneratedPassword = generatePassword({ length: 16 });
const analysis: PasswordStrengthResult = analyzePasswordStrength(result.password);
```

---

## Best Practices

### ✅ Do:

- Use passwords with at least 16 characters
- Include all character types (uppercase, lowercase, numbers, symbols)
- Use passphrases for high-security accounts
- Validate passwords in real-time with `quickStrengthCheck()`
- Provide actionable feedback from `analyzePasswordStrength()`
- Generate unique passwords for each service

### ❌ Don't:

- Don't use passwords shorter than 12 characters
- Don't reuse passwords across services
- Don't use personal information in passwords
- Don't skip strength validation
- Don't ignore security suggestions

---

## Security Notes

1. **Cryptographically Secure**: All passwords are generated using `crypto.getRandomValues()` from the Web Crypto API

2. **No Bias**: Implements rejection sampling to eliminate modulo bias

3. **Entropy Calculation**: Accurate mathematical calculation: log₂(charset_size^length)

4. **Pattern Detection**: Uses zxcvbn to detect keyboard patterns, repeated sequences, dates, and common passwords

5. **Zero Knowledge**: No passwords are logged, stored, or transmitted

---

## Troubleshooting

### Issue: Module not found

**Solution:**
```bash
# Install the package
npm install @ian-p1nt0/password-utils

# Or link local package
cd ..
npm pack
cd examples
npm install ../ian-p1nt0-password-utils-1.0.0.tgz
```

### Issue: Examples run but show errors

**Solution:**
Ensure you're using Node.js 20 or higher:
```bash
node --version  # Should be v20.0.0 or higher
```

---

## Contributing

Found an issue or want to add more examples? Please open an issue or pull request on GitHub:

- **Repository:** https://github.com/iAn-P1nt0/TrustVault-password-utils
- **Issues:** https://github.com/iAn-P1nt0/TrustVault-password-utils/issues

---

## License

These examples are provided under the same Apache-2.0 license as the main package.

---

**Happy Coding! 🔐**
