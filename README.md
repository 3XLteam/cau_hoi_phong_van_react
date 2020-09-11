# Tổng hợp câu hỏi phỏng vấn react
### 1.	Virtual DOM làm việc như thế nào trong React?  
Giống như actual DOM thật, virtual DOM ảo là node tree chứa tất cả element và content dưới dạng object và property.  
Method render() sẽ tạo ra virtual DOM từ các react component.  
React sẽ tạo mới virtual DOM mỗi khi có thay đổi data.  
#### Tóm tắt
1. Khi có sự thay đổi, toàn bộ UI sẽ được re-render vào virtual DOM.
2. React sẽ đo đạc sự khác nhau giữa actual DOM và virtual DOM.
3. Autual DOM sẽ được update dựa trên virtual DOM, chỉ update các phần bị thay đổi (patch)  
  
More info https://www.accelebrate.com/blog/the-real-benefits-of-the-virtual-dom-in-react-js
  
2.	Nêu rõ sự khác biệt giữa Virtual DOM và Shadow DOM.
3.	Nêu rõ vòng Lifecycle trong React, cho cả Class Component và Function Component.
4.	Higher-order component (HOC) là gì và ứng dụng trong React?
5.	Điểm mạnh và điểm yếu của React.
6.	React context là gì? Ứng dụng trong React?
7.	Server side rendering (SSR) hoạt động như thế nào? Làm sao để thực hiện SSR trong React?
8.	Stateless/Stateful Component là gì? Function Component là Stateless Component hay Stateful Component? Tại sao?
9.	Một project nên có bao nhiêu component là tối ưu nhất? Tại sao?
10.	Có sự khác biệt gì giữa Class Component, Pure Component và React.memo?
11.	Phân biệt Client Side Rendering (CRS), Server Side Rendering (SSR), Static Site Generator (SSG) và Progressive Web App (PWA).
12.	Redux là gì? Core principles của Redux là gì?
13.	Giới thiệu cách hoạt động của Redux.
14.	Có thể access Redux store từ bên ngoài component được ko? Giải thích.
15.	So sánh sự khác biệt giữa React Context và Redux.
16.	Redux Thunk, Redux Saga là gì? So sánh. Redux Thunk hay Redux Saga phù hợp nhất cho một project?
17.	Redux selector là gì? Tại sao sử dụng chúng?
18.	Có cách nào lưu trữ state trong store nhưng ko sử dụng Redux ko?
19.	Cho component tree như hình vẽ bên dưới.
Có mấy cách để khi user take action ở component D (vd click Submit form) thì component H sẽ nhận biết được event đó.
20.	Shallow Renderer là gì trong React testing?
21.	TestRederer package là gì trong React?
22.	Jest là gì? So sánh Jest và Jasmine.
