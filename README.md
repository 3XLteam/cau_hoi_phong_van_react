# Tổng hợp câu hỏi phỏng vấn react
### 1.	Virtual DOM làm việc như thế nào trong React?  
Giống như actual DOM thật, virtual DOM ảo là node tree chứa tất cả element và content dưới dạng object và property, được lưu vào memory. Method render() sẽ tạo ra virtual DOM từ các react component.  React sẽ tạo mới virtual DOM mỗi khi có thay đổi data.  
#### Tóm tắt
1. Khi có sự thay đổi, toàn bộ UI sẽ được re-render vào virtual DOM.
2. React sẽ đo đạc sự khác nhau giữa actual DOM và virtual DOM (diffing).
3. Autual DOM sẽ được update dựa trên virtual DOM, chỉ update các phần bị thay đổi (patch)  
  
More info https://www.accelebrate.com/blog/the-real-benefits-of-the-virtual-dom-in-react-js
  
### 2.	Nêu rõ sự khác biệt giữa Virtual DOM và Shadow DOM.

#### Giống nhau:
1. Giải quyết vấn đề performance khi sử dụng trực tiếp actual DOM.
2. Không xuất hiện trên actual DOM.

#### Khác nhau

Virual DOM | Shadow DOM
------------ | -------------
Là bản copy của toàn bộ actual DOM. | Là một phần nhỏ của actual DOM.
Là một chiến thuật (strategy) để tăng performance.| Là một công cụ (tool) để tăng performance.
Tách biệt với actual DOM. | Kết nối với actual DOM bằng shadow root.
Dùng để update nhanh và so sánh với actual DOM. | Dùng để tạo một môi trường độc lập, tách biệt với actual DOM (HTML, CSS).

More info
* https://www.blog.duomly.com/what-is-the-difference-between-shadow-dom-and-virtual-dom/
* https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM

### 3.	Nêu rõ vòng Lifecycle trong React, cho cả Class Component và Function Component.
Khi một components được khởi chạy nó sẽ phải trải qua 4 giai đoạn chính cho class component:
* initialization: Đây là giai đoạn mà thành phần sẽ bắt đầu hành trình của mình bằng cách khởi tạo state và props. Điều này thường được thực hiện bên trong phương thức constructor. Chỉ có một phương thức duy nhất: constructor.
* mounting: Giai đoạn này được thực hiện sau khi quá trình initialization(khởi tạo) được hoàn thành. Nó thực hiện nhiệm vụ chuyển virtual DOM (DOM ảo) trong React thành DOM và hiển thị trên trình duyệt. Component sẽ được render lần đầu tiên, ở đây chúng ta có 3 phương thức để tham gia vào giai đoạn này. Bao gồm các phương thức: componentWillMount, componentDidMount (thường call API ở lần render đầu tiên trong phương thức này).
* updating: Đây là giai đoạn thứ ba mà các component phải thực hiện, sau giai đoạn initialization (khởi tạo ) , mount (render lần đầu),... . Trong giai đoạn này, dữ liệu của các phần (props & state) sẽ được cập nhật để đáp ứng với các sự kiện của người dùng như click, gõ, v.v. Điều này dẫn đến việc re-render lại component, ở trong giai đoạn này chúng ta sẽ có 4 phương thức chính: shouldComponentUpdate (chỉ có khi dùng Component, không có khi dùng PureComponent), componentWillUpdate, componentDidUpdate
* unmounting: Đây là bước cuối cùng trong mỗi component, khi tất cả các tác vụ hoàn thành và bạn tiến hành unmount DOM. Chỉ có một phương thức duy nhất: componentWillUnmount.
Functional component không có lifecycle, nó chỉ sử dụng các hook tương ứng trong một số điều kiện nhất định có thể xem như tương đương với một phương thức.
### 4.	Higher-order component (HOC) là gì và ứng dụng trong React?

Giống với higher order function, HOC là một pattern phục vụ việc tái sử dụng logic trong React component. Là một component (HOC A) nhận param là một (B) hoặc nhiều component (C) rồi trả về một component mới (B v2, C v2). Trong đó B v2 và C v2 có chung một logic được nhận từ HOC A.

Cấu trúc HOC:
* Là một component.
* Nhận param component.
* Trả về một component.
* Component được trả về có thể render giống y chang param component.

#### Ví dụ:

1. Hiện loader khi đang đợi data

```javascript
import React from 'react';
function WithLoading(Component) {
  return function WihLoadingComponent({ isLoading, ...props }) {
    if (!isLoading) return <Component {...props} />;
    return <p>Hold on, fetching data might take some time.</p>;
  };
}

const ListWithLoading = WithLoading(List);

render() {
    return (
      <ListWithLoading
        isLoading={this.state.loading}
        repos={this.state.repos}
      />
    );
  }
```

2. Xử lý render theo tình trạng đăng nhập

```javascript
// withAuth.js
import React from "react";
function withAuth(Component) {
    return class AuthenticatedComponent extends React.Component {
        isAuthenticated() {
            return this.props.isAuthenticated;
        }
        render() {
            const loginErrorMessage = (
                <div>
                    Please <a href="/login">login</a> in order to view this part of the application.
                </div>
            );

            return (
                <div>
                    { this.isAuthenticated === true ? <Component {...this.props} /> : loginErrorMessage }
                </div>
            );
        }
    };
}
export default withAuth;

// MyProtectedComponent.js
import React from "react";
import {withAuth} from "./withAuth.js";
export class MyProectedComponent extends React.Component {
    render() {
        return (
            <div>
                This is only viewable  by authenticated users.
            </div>
        );
    }
}
export default withAuth(MyPrivateComponent);
```

3. Ép một style chung

```javascript
const withStyling = (BaseComponent) => (props) => (
  <BaseComponent {...props} style={{ fontWeight: 700, color: 'green' }} />
);

const HelloComponent = ({ name, ...otherProps }) => (
 <div {...otherProps}>Hello {name}!/div>
);

const EnhancedHello = withStyling(HelloComponent);
```

More info https://www.smashingmagazine.com/2020/06/higher-order-components-react/

### 5.	Điểm mạnh và điểm yếu của React.

Điểm mạnh | Điểm yếu
------------ | -------------
Virtual DOM (Nhanh + performance cao). | Poor documentation.
Reusable components.| Confusing JSX.
Downward data flow (prevents errors and facilitates debugging). | Complicated search engine optimization.
Huge community. | Narrow focus on UI.
React Developer Tools | 

### 6.	React context là gì? Ứng dụng trong React?

React context là một API của react, cho phép truyền props đi qua nhiều tầng của component tree mà không cần phải đi qua từng lớp component.
Nên sử dụng Context khi ta cần một data global, nhiều component trên những nhánh khác nhau cần sử dụng nó.
Ứng dụng: Thông tin đăng nhập, share style, theme...

### 7.	Server site rendering (SSR) hoạt động như thế nào? Làm sao để thực hiện SSR trong React?

SSR là khả năng render page trên server, khi server nhận request vào một page, nó sẽ chạy page này trên môi trường server (render, gọi API), khi page được render xong nó sẽ trả về cho browser, cộng việc của browser lúc này chỉ là hiện content của page được trả về lên cho user.  

Sử dụng nodejs, React.renderToString, React.hydrate để thực hiện SSR.

More info 
* https://www.digitalocean.com/community/tutorials/react-server-side-rendering
* https://ms314006.github.io/simple-implementing-ssr-in-react/

### 8.	Stateless/Stateful Component là gì? Function Component là Stateless Component hay Stateful Component? Tại sao?
* Stateless component (hay còn gọi là dump component) là các component không chứa state, chỉ sử dụng props (nếu có) để render ra UI.
* Stateful component (hay còn gọi là smart component) là các component có chứa state, logic và truyền props cho stateless component render ra UI.
* Trước khi có React hooks thì functional component được xem là stateless component (do không thể lưu lại state). Sau khi có React hooks thì functional component có thể được xem là stateful component vì có thể dùng state trong component với hook useState.
### 9.	Một project nên có bao nhiêu component là tối ưu nhất? Tại sao?
> TODO
### 10.	Có sự khác biệt gì giữa Class Component, Pure Component và React.memo?
> TODO
### 11.	Phân biệt Client Side Rendering (CRS), Server Side Rendering (SSR), Static Site Generator (SSG) và Progressive Web App (PWA).
> TODO
### 12.	Redux là gì? Core principles của Redux là gì?
> TODO
### 13.	Giới thiệu cách hoạt động của Redux.
> TODO
### 14.	Có thể access Redux store từ bên ngoài component được ko? Giải thích.
> TODO
### 15.	So sánh sự khác biệt giữa React Context và Redux.
> TODO
### 16.	Redux Thunk, Redux Saga là gì? So sánh. Redux Thunk hay Redux Saga phù hợp nhất cho một project?
> TODO
### 17.	Redux selector là gì? Tại sao sử dụng chúng?
> TODO
### 18.	Có cách nào lưu trữ state trong store nhưng ko sử dụng Redux ko?
> TODO
### 19.	Cho component tree như hình vẽ bên dưới. Có mấy cách để khi user take action ở component D (vd click Submit form) thì component H sẽ nhận biết được event đó.
> TODO
### 20.	Shallow Renderer là gì trong React testing?
> TODO
### 21.	TestRederer package là gì trong React?
> TODO
### 22.	Jest là gì? So sánh Jest và Jasmine.
> TODO
