---
layout: post
title: Notion Test
image: 8.jpg
date: 2023-01-17 13:35:20 +0200
tags:
categories: book
---


# Item 9. Prefer try-with-resources to try-finally

자바에는 close 메서드를 호출해 직접 닫아줘야 하는 자원이 많다. 이런 자원 중 상당수가 finalizer를 활용하고는 있지만 믿을만하지 못하다. try-finally가 많이 쓰이고 있다.

```java
static String firstLineOfFile(String path) throws IOException{
	BufferedReader br = new BufferedReader(new FileReader(path));
	try {
			return br.readLine();
	} finally {
			br.close();
	}
}

static void copy(String src, String dst) throws IOException {
		InputStream in = new FileInputStream(src);
		try {
			OutputStream out = new FileOutputStream(dst);
			try {
					byte[] buf = new byte[BUFFER_SIZE];
					int n;
					while((n = in.read(buf)) >= 0)
							out.write(buf, 0, n);
					} finally {
							out.close();
					}
				}finally {
						in.close();
				}
}
```

```java
static String firstLineOfFile(String path) throws IOException {
			try (BufferedReader br = new BufferedReader(new FileReader(path))) {
									return br.readLine();
			}
}

static void copy(String src, String dst) throws IOException {
					try (InputStream in = new FileInputStream(src);
							OutputStream out = new FileOutputStream(dst)) {
							byte[] buf = new byte[BUFFER_SIZE];
							int n;
							while((n = in.read(buf)) >= 0)
									out.write(buf, 0, n);
				}
}
```

<aside>
💡 **핵심 정리**
꼭 회수해야 하는 자원을 다룰 때는 try-finally 말고, try-with-resources를 사용하자. 예외는 없다. 코드는 더 짧고 분명해지고, 만들어지는 예외 정보도 훨씬 유용하다. try-finally로 작성하면 실용적이지 못할 만큼 코드가 지전분해지는 경우라도, try-with-resources로는 정확하고 쉽게 자원을 회수할 수 있다.

</aside>