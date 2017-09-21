# Memo Project [절차지향 - ArrayList 저장]
프로젝트를 구현하기 위해 아래와 같은 조건을 설정한 후 클래스 Memo를 사용해 쓰기, 읽기, 수정, 삭제, 전제 목록보기 기능이 있는 프로그램을 만들어보자.

## 조건
![flow](http://cfile22.uf.tistory.com/image/998A313359B50E423AE3FB)

## Memo Project [절차지향 - ArrayList]의 데이터 흐름
![flow](http://cfile10.uf.tistory.com/image/99C84D3359B5232C341D2F)
## 구현
```java
public class Main {
    // 데이터를 저장 할 ArrayList 설정
    ArrayList<Memo> list = new ArrayList<>();
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        OrgMemoMain main = new OrgMemoMain();

        // c(create)    : 데이터 입력모드로 전환
        // r(read)           : 데이터 읽기모드로 전환
        // u(update)     : 데이터 수정모드로 전환
        // d(delete)     : 데이터 삭제모드로 전환
        // l(list)        : 데이터 전체출력모드로 전환

        String command="";

        while(!command.equals("exit")) {
            System.out.println("---명령어 입력하세요---");
            System.out.println("c - 쓰기");
            System.out.println("r - 읽기");
            System.out.println("u - 수정");
            System.out.println("d - 삭제");
            System.out.println("l - 목록");
            System.out.println("exit - 종료");
            System.out.println("------------------");
            System.out.println("입력: " );

            command = scanner.nextLine();    

            switch(command) {
            case "c":
                main.create(scanner);
                break;
            case "r":
                main.read(scanner);
                break;
            case "u":
                main.update(scanner);
                break;
            case "d":
                main.delete(scanner);
                break;
            case "l":
                main.showAllData();
                break;
            }
        }

        System.out.println("종료");
    }

    // 데이터 입력
    public void create(Scanner sc) {
        // 객체 생성 (메모리 공간 확보)
        Memo item = new Memo();

        // 글번호
        item.no = list.size()+1;

        // 사용자로부터 데이터 입력
        System.out.println("이름을 입력하세요 : ");
        item.name = sc.nextLine();

        System.out.println("내용을 입력하세요 : ");
        item.content = sc.nextLine();

        item.datetime = System.currentTimeMillis();

        // 데이터 추가
        list.add(item);
    }

    // 데이터 읽기
    public void read(Scanner sc) {
        System.out.println("글 번호를 입력하세요");

        String tmpNo = sc.nextLine();
        int no = Integer.parseInt(tmpNo);

        // 입력 받은 번호의 데이터를 찾아 출력
        for (Memo item : list) {
            if (item.no == no) {
                System.out.println("No: " + item.no);
                System.out.println("Autor: " + item.name);
                System.out.println("Content: " + item.content);

                SimpleDateFormat sdf = new SimpleDateFormat("yyy-MM-dd hh:mm:ss");
                String formattedDate = sdf.format(item.datetime);
                System.out.println("Date: " + formattedDate);

                break;
            }
        }
    }

    // 데이터 업데이트
    // 업데이트의 경우, 해당 데이터를 덮어씌우므로 문제 해결이 가능
    public void update(Scanner sc) {
        // 숫자 입력 예외 처리
        String tmpNo = sc.nextLine();
        int no = Integer.parseInt(tmpNo);

        for (Memo item : list) {
            if (item.no == no) {
                System.out.println("이름을 입력하세요 : ");
                item.name = sc.nextLine();

                System.out.println("내용을 입력하세요 : ");
                item.content = sc.nextLine();

                // 날짜
                item.datetime = System.currentTimeMillis();
                break;    

            }
        }
    }

    // 데이터 삭제
    public void delete(Scanner sc) {
        System.out.println("글 번호를 입력하세요");

        // 숫자 입력 예외 처리
        String tmpNo = sc.nextLine();
        int no = Integer.parseInt(tmpNo);

        for (Memo item : list) {
            if (item.no == no) {
                System.out.println("No: " + item.no);
                System.out.println("Autor: " + item.name);
                System.out.println("Content: " + item.content);

                SimpleDateFormat sdf = new SimpleDateFormat("yyy-MM-dd hh:mm:ss");
                String formattedDate = sdf.format(item.datetime);
                System.out.println("Date: " + formattedDate);

                System.out.println("해당 글을 삭제 완료");

                // 해당 데이터 삭제
                list.remove(item);

                break;
            }
        }
    }

    public void showAllData() {
        // ArrayList 저장소 내역 출력
        for (Memo item : list) {
            System.out.println("No: " + item.no);
            System.out.println("Auth: " + item.name);
            System.out.println("Content: " + item.content);
        }
    }
}

// 조건으로 설정한 Memo class
class Memo {
    int no;
    String name;
    String content;
    long datetime;
}

```
