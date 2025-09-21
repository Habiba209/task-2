from PIL import Image

def encrypt_image(input_path, output_path, key):
    img = Image.open(input_path)
    pixels = img.load()  # access pixels

    for i in range(img.size[0]):  # width
        for j in range(img.size[1]):  # height
            r, g, b = pixels[i, j]

            # Simple XOR encryption with key
            r = r ^ key
            g = g ^ key
            b = b ^ key

            pixels[i, j] = (r, g, b)

    img.save(output_path)
    print(f"Image encrypted and saved as {output_path}")


def decrypt_image(input_path, output_path, key):
    # Since XOR is reversible, decryption is same as encryption
    encrypt_image(input_path, output_path, key)


def main():
    print("===== Image Encryption Tool =====")
    choice = input("Do you want to (E)ncrypt or (D)ecrypt? ").strip().lower()
    input_path = input("Enter input image path (e.g., test.jpg): ").strip()
    output_path = input("Enter output image path (e.g., result.jpg): ").strip()
    key = int(input("Enter encryption key (0-255): "))

    if choice in ["e", "encrypt"]:
        encrypt_image(input_path, output_path, key)

    elif choice in ["d", "decrypt"]:
        decrypt_image(input_path, output_path, key)

    else:
        print("❌ Invalid choice! Please select E or D.")


if _name_ == "_main_":
    main()
