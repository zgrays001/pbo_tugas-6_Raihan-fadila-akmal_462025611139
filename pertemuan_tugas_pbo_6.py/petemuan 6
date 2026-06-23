
class ElectricCar(LandVehicle, ElectricVehicle):
    """
    Mobil listrik — mewarisi KEDUANYA (LandVehicle & ElectricVehicle).
 
    Diamond Problem:
        Tanpa MRO (Method Resolution Order) Python + super(), konstruktor
        Vehicle.__init__ bisa terpanggil DUA KALI.
        Python menyelesaikannya dengan C3-linearization MRO sehingga
        Vehicle.__init__ hanya terpanggil SEKALI.
 
    MRO ElectricCar:
        ElectricCar → LandVehicle → ElectricVehicle → Vehicle → object
    """
 
    def __init__(self, brand: str, model: str, year: int,
                 wheels: int, battery_kwh: float, autopilot: bool = False):
 
        # super() mengikuti MRO → LandVehicle.__init__ dipanggil pertama,
        # yang kemudian meneruskan ke ElectricVehicle.__init__ via super(),
        # lalu ke Vehicle.__init__ — hanya SEKALI, itulah solusi diamond!
        #
        # Namun LandVehicle & ElectricVehicle masing-masing punya parameter
        # berbeda, jadi kita perlu memanggil keduanya secara eksplisit:
        LandVehicle.__init__(self, brand, model, year, wheels)
        ElectricVehicle.__init__(self, brand, model, year, battery_kwh)
 
        self.autopilot = autopilot
        print(f"  [ElectricCar.__init__] → Autopilot: {'Aktif' if autopilot else 'Tidak aktif'}")
 
    def describe(self):
        # Panggil describe dari kedua parent melalui super() mengikuti MRO
        LandVehicle.describe(self)
        ElectricVehicle.describe(self)
        print(f"  [ElectricCar.describe] Fitur autopilot: {'Aktif' if self.autopilot else 'Tidak aktif'}.")
 
    def full_status(self):
        print("=" * 55)
        print(f"  STATUS KENDARAAN: {self.info()}")
        print("=" * 55)
        self.describe()
        print("-" * 55)
 


def main():
    print("\n" + "=" * 55)
    print("  DEMO 1: LandVehicle (Kelas B)")
    print("=" * 55)
    motor = LandVehicle("Honda", "Vario 160", 2023, wheels=2)
    motor.start()
    motor.describe()
    motor.stop()
 
    print("\n" + "=" * 55)
    print("  DEMO 2: ElectricVehicle (Kelas C)")
    print("=" * 55)
    scooter = ElectricVehicle("Gesits", "G1", 2022, battery_kwh=1.2)
    scooter.start()
    scooter.charge()
    scooter.describe()
 
    print("\n" + "=" * 55)
    print("  DEMO 3: ElectricCar — Diamond Problem (Kelas D)")
    print("=" * 55)
    tesla = ElectricCar(
        brand="Tesla", model="Model 3",
        year=2024, wheels=4,
        battery_kwh=75.0, autopilot=True
    )
    tesla.full_status()
    tesla.start()
    tesla.charge()
    tesla.stop()
 
    print("\n" + "=" * 55)
    print("  Method Resolution Order (MRO) — ElectricCar")
    print("=" * 55)
    for i, cls in enumerate(ElectricCar.__mro__):
        print(f"  {i + 1}. {cls}")
 
    print("\n  ✅ Diamond Problem berhasil diatasi dengan MRO Python!")
    print("     Vehicle.__init__ dipanggil hanya SATU KALI.\n")
 
 
if __name__ == "__main__":
    main()
 
