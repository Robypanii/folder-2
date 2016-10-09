# folder-2
master; void initSPI_Master() {
DDRB |= (1<<2)|(1<<3)|(1<<5); // SCK, MOSI dan SS menjadi output DDRB &= ~(1<<4); // MISO menjadi input SPCR |= (1<<MSTR); // SPI sebagai master SPCR |= (1<<SPR0)|(1<<SPR1); // Pembagi clock = 128 SPCR |= (1<<SPE); // Aktifkan SPI
}
void setup() {
initSPI_Master();
pinMode(2, INPUT); pinMode(3, INPUT); pinMode(4, INPUT); digitalWrite(2, HIGH); digitalWrite(3, HIGH); digitalWrite(4, HIGH); } void loop() { if(digitalRead(2)==LOW) { kirimData("Hallo\r\n"); } else if(digitalRead(3)==LOW) { kirimData("Apa\r\n"); } else if(digitalRead(4)==LOW) { kirimData("Kabar\r\n"); } } void kirimData(char *string) { int panjangString = strlen(string); for(int i=0; i<panjangString; i++) { SPDR = string[i]; while(!(SPSR & (1<<SPIF))); delay(10); } }

slave ;

include

LiquidCrystal lcd(A0, A1, A2, A3, A4, A5); String dataString = ""; char data; void initSPI_Slave() {
DDRB &= ~((1<<2)|(1<<3)|(1<<5)); // SCK, MOSI dan SS me njadi input DDRB |= (1<<4); // MISO menjadi output SPCR &= ~(1< "); lcd.setCursor(0,1); lcd.print(dataString); // Menampilkan string ke LCD dataString = ""; }

}

void initSPI_Master() {
DDRB |= (1<<2)|(1<<3)|(1<<5); // SCK, MOSI dan SS menj adi output DDRB &= ~(1<<4); // MISO menjadi input SPCR |= (1<<MSTR); // SPI sebagai master SPCR |= (1<<SPR0)|(1<<SPR1); // Pembagi clock = 128 SPCR |= (1<<SPE); // Aktifkan SPI
}
void setup() {
initSPI_Master();
pinMode(2, INPUT); pinMode(3, INPUT); pinMode(4, INPUT); digitalWrite(2, HIGH); digitalWrite(3, HIGH); digitalWrite(4, HIGH); } void loop() { if(digitalRead(2)==LOW) kirimData(5); else if(digitalRead(3)==LOW) kirimData(10); else if(digitalRead(4)==LOW) kirimData(15); } void kirimData(unsigned char data) { SPDR = data; // Kirim data while(!(SPSR & (1<<SPIF))); // Tunggu sampai pengiriman selesai delay(50);

}

include

LiquidCrystal lcd(A0, A1, A2, A3, A4, A5); unsigned char data; void initSPI_Slave() { DDRB &= ~((1<<2)|(1<<3)|(1<<5)); // SCK, MOSI dan SS menjadi input DDRB |= (1<<4); // MISO menjadi output SPCR &= ~(1< "); lcd.setCursor(0,1); lcd.print(data,HEX); }

Tugas & Pertanyaan ; 1. 2 = 5 3 = A 4 = F 2. 2 = HALLO 3 = APA 4 = KABAR
