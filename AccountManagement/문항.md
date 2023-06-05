아래에 Java를 사용하여 계좌 관리 프로그램을 구현한 예시 코드를 제공합니다. 이 예시 코드는 ArrayList 대신 배열을 사용하여 계좌를 관리합니다.

```java
import java.util.Scanner;

class Account {
    private String accountNumber;
    private double balance;

    public Account(String accountNumber, double balance) {
        this.accountNumber = accountNumber;
        this.balance = balance;
    }

    public String getAccountNumber() {
        return accountNumber;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        balance += amount;
        System.out.println(amount + "원이 입금되었습니다.");
    }

    public void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println(amount + "원이 출금되었습니다.");
        } else {
            System.out.println("잔액이 부족합니다.");
        }
    }
}

class AccountManagement {
    private Account[] accountList;
    private int numAccounts;
    private Scanner scanner;

    public AccountManagement(int maxSize) {
        accountList = new Account[maxSize];
        numAccounts = 0;
        scanner = new Scanner(System.in);
    }

    public void addAccount(String accountNumber, double balance) {
        Account account = new Account(accountNumber, balance);
        accountList[numAccounts] = account;
        numAccounts++;
        System.out.println("계좌가 추가되었습니다.");
    }

    public void showAccountList() {
        System.out.println("계좌 목록:");
        for (int i = 0; i < numAccounts; i++) {
            Account account = accountList[i];
            System.out.println("계좌번호: " + account.getAccountNumber() + ", 잔액: " + account.getBalance() + "원");
        }
    }

    public void deposit(String accountNumber, double amount) {
        Account account = findAccount(accountNumber);
        if (account != null) {
            account.deposit(amount);
        } else {
            System.out.println("해당 계좌를 찾을 수 없습니다.");
        }
    }

    public void withdraw(String accountNumber, double amount) {
        Account account = findAccount(accountNumber);
        if (account != null) {
            account.withdraw(amount);
        } else {
            System.out.println("해당 계좌를 찾을 수 없습니다.");
        }
    }

    private Account findAccount(String accountNumber) {
        for (int i = 0; i < numAccounts; i++) {
            Account account = accountList[i];
            if (account.getAccountNumber().equals(accountNumber)) {
                return account;
            }
        }
        return null;
    }

    public void run() {
        while (true) {
            System.out.println("\n=== 계좌 관리 프로그램 ===");
            System.out.println("1. 계좌 추가");
            System.out.println("2. 계좌 목록 조회");
            System.out.println("3. 입금");
            System.out.println("4. 출금");
            System.out.println("0. 종료");
            System.out.print("원하는 기능을 선택하세요: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // 개행 문자 제거

            if (choice == 0) {
                System.out.println("프로그램을 종료합니다.");
                break;
            }

            switch (choice) {
                case 1:
                    System.out.print("계좌번호: ");
                    String accountNumber = scanner.nextLine();
                    System.out.print("잔액: ");
                    double balance = scanner.nextDouble();
                    scanner.nextLine(); // 개행 문자 제거
                    addAccount(accountNumber, balance);
                    break;
                case 2:
                    showAccountList();
                    break;
                case 3:
                    System.out.print("계좌번호: ");
                    accountNumber = scanner.nextLine();
                    System.out.print("입금액: ");
                    double depositAmount = scanner.nextDouble();
                    scanner.nextLine(); // 개행 문자 제거
                    deposit(accountNumber, depositAmount);
                    break;
                case 4:
                    System.out.print("계좌번호: ");
                    accountNumber = scanner.nextLine();
                    System.out.print("출금액: ");
                    double withdrawAmount = scanner.nextDouble();
                    scanner.nextLine(); // 개행 문자 제거
                    withdraw(accountNumber, withdrawAmount);
                    break;
                default:
                    System.out.println("잘못된 입력입니다. 다시 입력해주세요.");
                    break;
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        AccountManagement accountManagement = new AccountManagement(100);
        accountManagement.run();
    }
}
```

이 예시 코드를 실행하면 계좌 관리 프로그램이 시작됩니다. 메뉴에서 원하는 기능을 선택하고 각 기능에 맞게 입력을 진행하면 계좌를 추가하거나 조회하고 입금 및 출금을 수행할 수 있습니다. 프로그램을 종료하려면 메뉴에서 0을 선택하면 됩니다.

이 예시 코드를 실행하고 나서 직접 계좌를 추가하고 관리해 보세요. 계좌 목록 조회, 입금, 출금 기능이 제대로 동작하는지 확인할 수 있을 것입니다.
