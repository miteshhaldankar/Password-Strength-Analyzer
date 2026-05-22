# Password-Strength-Analyzer
Developed a password analysis tool that evaluates strength based on length, character variety, and entropy. Implemented UI using Tkinter and provided real-time feedback and security suggestions.

import re

def password_strength(password):
    suggestions = []
    score = 0

    # Length check
    if len(password) >= 12:
        score += 2
    elif len(password) >= 8:
        score += 1
    else:
        suggestions.append("Increase password length to at least 12 characters.")

    # Lowercase letters
    if re.search(r"[a-z]", password):
        score += 1
    else:
        suggestions.append("Add lowercase letters.")

    # Uppercase letters
    if re.search(r"[A-Z]", password):
        score += 1
    else:
        suggestions.append("Add uppercase letters.")

    # Digits
    if re.search(r"\d", password):
        score += 1
    else:
        suggestions.append("Add numbers.")

    # Special characters
    if re.search(r"[!@#$%^&*()_+=\-{}[\]:;\"'<>,.?/~`|\\]", password):
        score += 1
    else:
        suggestions.append("Add special characters.")

    # Avoid common passwords
    common_passwords = ['password', '123456', 'qwerty', 'abc123', '111111']
    if password.lower() in common_passwords:
        suggestions.append("Avoid using common or easily guessable passwords.")
        score = 0  # override score for common passwords

    # Avoid repetitive characters
    if re.search(r"(.)\1{2,}", password):
        suggestions.append("Avoid repeating characters.")

    # Strength label
    if score <= 2:
        strength = "Very Weak"
    elif score == 3:
        strength = "Weak"
    elif score == 4:
        strength = "Moderate"
    elif score == 5:
        strength = "Strong"
    else:
        strength = "Very Strong"

    return strength, suggestions


# Main execution
if __name__ == "__main__":
    password = input("Enter your password to check: ")
    strength, tips = password_strength(password)

    print(f"\nPassword Strength: {strength}")
    if tips:
        print("Suggestions to improve your password:")
        for tip in tips:
            print(f" - {tip}")
    else:
        print("Your password looks strong!")
