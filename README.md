# Question1-Accommodation-Area
Java program for calculating gym and swimming area charges
import java.util.Scanner;

abstract class Area {
    protected String name;
    protected int occupants;
    protected boolean[] lights = new boolean[3]; // 3 lights

    public Area(String name) {
        this.name = name;
        this.occupants = 0;
        for (int i = 0; i < lights.length; i++) lights[i] = false;
    }

    public String getName() { return name; }
    public int getOccupants() { return occupants; }
    public boolean getLight(int i) { return lights[i]; }

    public void addOccupants(int n) {
        if (n > 0) occupants += n;
    }

    public void removeOccupants(int n) {
        if (n > 0) occupants = Math.max(0, occupants - n);
    }

    public boolean switchOnLight(int number) {
        if (number >= 1 && number <= 3) {
            lights[number - 1] = true;
            return true;
        }
        return false;
    }

    public boolean switchOffLight(int number) {
        if (number >= 1 && number <= 3) {
            lights[number - 1] = false;
            return true;
        }
        return false;
    }

    public String statusReport() {
        StringBuilder sb = new StringBuilder();
        sb.append("Area: ").append(name).append("\n");
        sb.append("Occupants: ").append(occupants).append("\n");
        for (int i = 0; i < 3; i++) {
            sb.append("Light ").append(i + 1).append(": ")
              .append(lights[i] ? "ON" : "OFF").append("\n");
        }
        return sb.toString();
    }
}

class GymArea extends Area {
    public GymArea() { super("Gym"); }
}

class SwimmingArea extends Area {
    public SwimmingArea() { super("Swimming Pool"); }
}

// Removed public so filename can be Main.java
class AccommodationController {
    private static Scanner scanner = new Scanner(System.in);

    private static int readInt(String prompt) {
        while (true) {
            System.out.print(prompt);
            try {
                int v = Integer.parseInt(scanner.nextLine().trim());
                return v;
            } catch (NumberFormatException e) {
                System.out.println("Invalid integer. Try again.");
            }
        }
    }

    private static String readCommand(String prompt) {
        System.out.print(prompt);
        return scanner.nextLine().trim().toUpperCase();
    }

    public static void main(String[] args) {
        Area gym = new GymArea();
        Area pool = new SwimmingArea();
        Area active = gym; // default

        System.out.println("Accommodation Areas Controller");
        System.out.println("Active area is: " + active.getName());

        boolean running = true;
        while (running) {
            System.out.println("\nMenu:");
            System.out.println("S – Select active area (G = Gym, P = Swimming)");
            System.out.println("W – Add n occupants");
            System.out.println("X – Remove n occupants");
            System.out.println("Y – Switch ON light (1–3)");
            System.out.println("Z – Switch OFF light (1–3)");
            System.out.println("R – Report status");
            System.out.println("Q – Quit");

            String cmd = readCommand("Enter option: ");

            switch (cmd) {
                case "S":
                    String which = readCommand("Select area (G for Gym, P for Swimming): ");
                    if ("G".equals(which)) active = gym;
                    else if ("P".equals(which)) active = pool;
                    else {
                        System.out.println("Unknown selection. Use G or P.");
                        break;
                    }
                    System.out.println("Active area set to: " + active.getName());
                    break;

                case "W":
                    int add = readInt("Enter number of occupants to add: ");
                    if (add < 0) System.out.println("Enter positive integer only.");
                    else {
                        active.addOccupants(add);
                        System.out.println("Added " + add + " occupants. Total now: " + active.getOccupants());
                    }
                    break;

                case "X":
                    int rem = readInt("Enter number of occupants to remove: ");
                    if (rem < 0) System.out.println("Enter positive integer only.");
                    else {
                        active.removeOccupants(rem);
                        System.out.println("Removed " + rem + " occupants (if available). Total now: " + active.getOccupants());
                    }
                    break;

                case "Y":
                    int on = readInt("Enter light number to switch ON (1-3): ");
                    if (!active.switchOnLight(on)) System.out.println("Light number must be 1, 2 or 3.");
                    else System.out.println("Light " + on + " is now ON in " + active.getName());
                    break;

                case "Z":
                    int off = readInt("Enter light number to switch OFF (1-3): ");
                    if (!active.switchOffLight(off)) System.out.println("Light number must be 1, 2 or 3.");
                    else System.out.println("Light " + off + " is now OFF in " + active.getName());
                    break;

                case "R":
                    System.out.println("\nStatus Report:\n" + active.statusReport());
                    break;

                case "Q":
                    System.out.println("Quitting program. Goodbye.");
                    running = false;
                    break;

                default:
                    System.out.println("Unknown option. Please enter S, W, X, Y, Z, R or Q.");
            }
        }
        scanner.close();
    }
}![IMG-20251019-WA0244](https://github.com/user-attachments/assets/5c50d3cc-d43a-43f3-bd15-ed5ed53afaba)
![IMG-20251019-WA0242](https://github.com/user-attachments/assets/70859f6c-16ec-4e42-b790-82b6027edc6c)
![IMG-20251019-WA0240](https://github.com/user-attachments/assets/ed324a8e-0c2e-4101-9df3-46c541e0c9d9)
![IMG-20251019-WA0219](https://github.com/user-attachments/assets/407e73b1-9799-4646-af4e-fb21df04df71)
