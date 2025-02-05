from PIL import Image
import numpy as np
import os


def encrypt_image(image_path, key):
    try:
        if not (0 <= key <= 255):
            raise ValueError("Key must be between 0 and 255.")
        img = Image.open(image_path)
        img_array = np.array(img)
        encrypted_array = np.bitwise_xor(img_array, key)
        encrypted_image = Image.fromarray(encrypted_array.astype(np.uint8))
        encrypted_image_path = os.path.splitext(image_path)[0] + "_encrypted.png"
        encrypted_image.save(encrypted_image_path)
        print(f"Encryption successful! Image saved at {encrypted_image_path}")
    except Exception as e:
        print("Error during encryption:", e)


def decrypt_image(encrypted_image_path, key):
    try:
        if not (0 <= key <= 255):
            raise ValueError("Key must be between 0 and 255.")
        img = Image.open(encrypted_image_path)
        img_array = np.array(img)
        decrypted_array = np.bitwise_xor(img_array, key)
        decrypted_image = Image.fromarray(decrypted_array.astype(np.uint8))
        decrypted_image_path = os.path.splitext(encrypted_image_path)[0] + "_decrypted.png"
        decrypted_image.save(decrypted_image_path)
        print(f"Decryption successful! Image saved at {decrypted_image_path}")
    except Exception as e:
        print("Error during decryption:", e)


def main():
    print("Image Encryption and Decryption Tool")
    print("1. Encrypt Image")
    print("2. Decrypt Image")
    choice = input("Select an option (1/2): ")
    if choice == "1":
        image_path = input("Enter the path to the image: ")
        key = int(input("Enter an encryption key (0-255): "))
        encrypt_image(image_path, key)
    elif choice == "2":
        encrypted_image_path = input("Enter the path to the encrypted image: ")
        key = int(input("Enter the decryption key (0-255): "))
        decrypt_image(encrypted_image_path, key)
    else:
        print("Invalid option. Exiting.")


if __name__ == "__main__":
    main()
