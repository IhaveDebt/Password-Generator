package main

import (
	"crypto/rand"
	"fmt"
	"math/big"
)

func generatePassword(length int, useSymbols bool) string {
	letters := "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
	if useSymbols {
		letters += "!@#$%^&*()-_=+[]{}<>?/|"
	}

	password := make([]byte, length)
	for i := range password {
		num, _ := rand.Int(rand.Reader, big.NewInt(int64(len(letters))))
		password[i] = letters[num.Int64()]
	}
	return string(password)
}

func main() {
	var length int
	var useSymbols string

	fmt.Print("Enter password length: ")
	fmt.Scanln(&length)

	fmt.Print("Include symbols? (y/n): ")
	fmt.Scanln(&useSymbols)

	password := generatePassword(length, useSymbols == "y")
	fmt.Println("Generated Password:", password)
}
