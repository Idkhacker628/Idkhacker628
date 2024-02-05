- 👋 Hi, I’m @Idkhacker628
    - 👀 I’m interested in hacking 
- 🌱 I’m currently learning nothing 
- 📫 How to reach me email noahelmoghazi2031@gmail.com
i made a game if u want to play it
<!---
Idkhacker628/Idkhacker628 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
---
1'
import java.util.Random;
import java.util.Scanner;

public class ZombieSurvivalGame {
    private static final int MAX_HEALTH = 100;
    private static final int MAX_HUNGER = 100;
    private static final int EVENT_CHANCE = 30;

    private int health;
    private int hunger;
    private int ammo;
    private Random random;
    private Scanner scanner;

    public ZombieSurvivalGame() {
        health = 100;
        hunger = MAX_HUNGER;
        ammo = 10;
        random = new Random();
        scanner = new Scanner(System.in);
    }

    private void displayStatus() {
        System.out.println("Health: " + health);
        System.out.println("Hunger: " + hunger);
        System.out.println("Ammo: " + ammo);
    }

    private void handleRandomEvent() {
        if (random.nextInt(100) < EVENT_CHANCE) {
            int eventImpact = random.nextInt(20) + 1;  // Random impact between 1 and 20
            int healthImpact = random.nextBoolean() ? -eventImpact : eventImpact; // Randomly positive or negative
            int hungerImpact = random.nextBoolean() ? -eventImpact : eventImpact;

            System.out.println("Random event occurred!");

            if (health + healthImpact > 0 && health + healthImpact <= MAX_HEALTH) {
                health += healthImpact;
                System.out.println("Health " + (healthImpact > 0 ? "increased" : "decreased") + " by " + Math.abs(healthImpact));
            }

            if (hunger + hungerImpact >= 0 && hunger + hungerImpact <= MAX_HUNGER) {
                hunger += hungerImpact;
                System.out.println("Hunger " + (hungerImpact > 0 ? "increased" : "decreased") + " by " + Math.abs(hungerImpact));
            }
        }
    }

    private void survive() {
        while (health > 0) {
            displayStatus();
            handleRandomEvent();

            System.out.println("Choose an action: 1. Eat 2. Rest 3. Use Gun 4. Quit");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    eat();
                    break;
                case 2:
                    rest();
                    break;
                case 3:
                    useGun();
                    break;
                case 4:
                    System.out.println("Game over. Thanks for playing!");
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid choice. Try again.");
            }

            // Simulate the passage of time
            hunger--;
            if (hunger <= 0) {
                System.out.println("You died of hunger. Game over.");
                System.exit(0);
            }
        }
    }

    private void eat() {
        System.out.println("You ate some food.");
        hunger += 10; // Increase hunger when eating
    }

    private void rest() {
        System.out.println("You rested.");
        health += 5; // Increase health when resting
    }

    private void useGun() {
        if (ammo > 0) {
            System.out.println("You encountered a zombie!");
            System.out.println("Shoot the zombie? (1. Yes / 2. No)");
            int shootChoice = scanner.nextInt();

            if (shootChoice == 1) {
                System.out.println("You shot the zombie!");
                ammo--;
            } else {
                System.out.println("You decided not to shoot. The zombie attacked you!");
                health -= 10;
            }
        } else {
            System.out.println("You're out of ammo! Find more ammo to continue using the gun.");
        }
    }

    public static void main(String[] args) {
        ZombieSurvivalGame game = new ZombieSurvivalGame();
        game.survive();
    }
}