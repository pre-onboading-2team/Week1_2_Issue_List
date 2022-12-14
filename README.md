# Week 1-2. issue list

1. [ν μκ° π«](#1-ν-μκ°-)
2. [νλ‘μ νΈ μκ° π](#2-νλ‘μ νΈ-μκ°-)
3. [κΈ°μ  μ€ν π ](#3-κΈ°μ -μ€ν-)
4. [κ΅¬ν κΈ°λ₯ π](#4-κ΅¬ν-κΈ°λ₯-)
5. [νλ‘μ νΈ κ΅¬μ‘° π](#5-νλ‘μ νΈ-κ΅¬μ‘°-)
6. [Best Practice μ μ κ³Όμ π©βπ¦βπ¦](#6-best-practice-μ μ κ³Όμ )
7. [νλ‘μ νΈ μ€μΉ λ° μ€ν β¨](#7-νλ‘μ νΈ-μ€μΉ-λ°-μ€ν-)  

<br/>

- [π λ°°ν¬ λ§ν¬](https://2nd-assignment.vercel.app/)
- [π ν λΈμ](https://plain-airboat-3f4.notion.site/10-27-Todo-f9fb2a1265e54c33b0b73c306c230042)

<br />



## 1. ν μκ° π«

- [μ΄λΉλ (νμ₯)](https://github.com/bitnaleeeee)
- [λͺ¨μλΉ](https://github.com/Topbin2)
- [κΉμ§μ](https://github.com/genuine-seok)
- [λ°μ°λΉ](https://github.com/Debonchocola)
- [μ΄μμ°](https://github.com/strongpond)
- [μ‘°μ±νΈ](https://github.com/CSH111)
- [μ λμ](https://github.com/eodnjs467)

<br />

## 2. νλ‘μ νΈ μκ° π

- κ°μ : μν°λ νλ‘ νΈμλ νλ¦¬μ¨λ³΄λ© 7κΈ° 1ν κ³Όμ  1-2 μ€ Best Practice
- μ£Όμ  : νΉμ  κΉν λ νμ§ν λ¦¬μ μ΄μ λͺ©λ‘κ³Ό μμΈ λ΄μ©μ νμΈνλ μΉ μ¬μ΄νΈ κ΅¬μΆ
- κΈ°κ° : 2022.10.29 ~ 2022.10.30

<br />


## 3. κΈ°μ  μ€ν π 

- React
- Typescript
- Styled-Components

<br />

## 4. κ΅¬ν κΈ°λ₯ π

- μ΄μ λͺ©λ‘ νμ΄μ§ κ΅¬ν
  - λ¬΄νμ€ν¬λ‘€
  - κ΄κ³ λ°°λ μ½μ
- μμΈ μ΄μ νμ΄μ§ κ΅¬ν
- Context APIλ₯Ό νμ©ν μ΄μ μνκ΄λ¦¬ λ° API μ°λ
- λ°μ΄ν° μμ²­ μ€ λ‘λ© νμ
- μλ¬ νλ©΄ κ΅¬ν
- μ§μ μ‘°κ±΄μ λ§κ² λ°μ΄ν° μμ²­ λ° νμ
- λ°μν μΉ κ΅¬ν

<br />

## 5. νλ‘μ νΈ κ΅¬μ‘° π

```bash
src
βββ apis  // issue κ΄λ ¨ api service μμ²­
βββ assets  // μ μ­ μ€νμΌλ§
βββ components  // κ³΅μ© μ»΄ν¬λνΈ
βββ context // issue μνκ΄λ¦¬ context
βββ hooks // scroll κ΄λ ¨ μ»€μ€ν ν
βββ pages // νμ΄μ§ λ° νμ΄μ§ κ³ μ  μ»΄ν¬λνΈ
βββ types // κ³΅μ©νμ κ΄λ¦¬
βββ utils // dateformatting, axios κ΄λ ¨ μ νΈ ν¨μ
```

<br/>


## 6. Best Practice μ μ κ³Όμ π©βπ¦βπ¦

  ### μ μ μ΄μ  1 - λ¬΄νμ€ν¬λ‘€
  
  ```javascript
export const useInfiniteScroll = (
  onIntersect: () => void,
  options?: IntersectionObserverInit
) => {
  const [target, setTarget] = useState<Element | null>(null);

  const handleIntersect = useCallback(
    ([entry]: IntersectionObserverEntry[]) => {
      if (entry.isIntersecting) {
        onIntersect();
      }
    },
    [onIntersect]
  );

  useEffect(() => {
    const observer = new IntersectionObserver(handleIntersect, options);
    target && observer.observe(target);
    return () => {
      observer.disconnect();
    };
  }, [handleIntersect, target, options]);

  return [setTarget];
};
```
#### μ½λ©νΈ
  - `Intersection Opserver API` νμ©ν΄ scrollEventλ₯Ό μ΄μ©ν κ²μ λΉν΄ μ΅μ νλ₯Ό ν¨μ¨μ μΌλ‘ μ μ©ν μ μ΄ μ’μμ΅λλ€. - λ°μ°λΉ
  - μ¬μ¬μ©μ±μ μν΄ μ»€μ€ννμΌλ‘ λΆλ¦¬ν λΆλΆμ΄ μ’μμ΅λλ€. - κΉμ§μ

<br>

### μ μ μ΄μ  2 - Context APIλ₯Ό νμ©ν API μ°λ
- `Context API` `useReducer` λ₯Ό νμ©νμ¬ `Flux ν¨ν΄`μΌλ‘ μλ² λ°μ΄ν° κ΄λ¦¬ 

```javascript
export enum IssueActionTypes {
  GET_ISSUE_LIST_SUCCESS = "GET_ISSUES_LIST_SUCCESS",
  GET_ISSUE_LIST_LOADING = "GET_ISSUES_LIST_LOADING",
  GET_ISSUE_LIST_ERROR = "GET_ISSUES_LIST_ERROR",

  GET_ISSUE_DETAIL_SUCCESS = "GET_ISSUES_DETAIL_SUCCESS",
  GET_ISSUE_DETAIL_LOADING = "GET_ISSUES_DETAIL_LOADING",
  GET_ISSUE_DETAIL_ERROR = "GET_ISSUES_DETAIL_ERROR",
}

const initialState: IssueCtxInitialState = {
  isLoading: false,
  isError: false,
  issueList: [],
  issueDetail: null,
};

const issueReducer = (
  state: IssueCtxInitialState,
  action: { type: IssueActionTypes; data?: Issue[] | Issue }
) => {
  switch (action.type) {
    case IssueActionTypes.GET_ISSUE_LIST_LOADING:
      return {
        ...state,
        isLoading: true,
        isError: false,
      };
    case IssueActionTypes.GET_ISSUE_LIST_SUCCESS:
      return {
        ...state,
        issueList: [...state.issueList, ...(action.data as Issue[])],
        isLoading: false,
        isError: false,
      };
    case IssueActionTypes.GET_ISSUE_LIST_ERROR:
      return {
        ...state,
        isLoading: false,
        isError: true,
      };
    case IssueActionTypes.GET_ISSUE_DETAIL_LOADING:
      return {
        ...state,
        isLoading: true,
        isError: false,
      };
    case IssueActionTypes.GET_ISSUE_DETAIL_SUCCESS:
      return {
        ...state,
        issueDetail: action.data as Issue,
        isLoading: false,
        isError: false,
      };
    case IssueActionTypes.GET_ISSUE_DETAIL_ERROR:
      return {
        ...state,
        isLoading: false,
        isError: true,
      };
    default:
      throw new Error("action typeμ νμΈν΄μ£ΌμΈμ.");
  }
};

const IssueStateContext = createContext<IssueCtxInitialState>(initialState);
const IssueDispatchContext = createContext<React.Dispatch<{
  type: IssueActionTypes;
  data?: Issue[] | Issue;
}> | null>(null);

export const IssueProvider = ({ children }: { children: JSX.Element }) => {
  const [state, dispatch] = useReducer(issueReducer, initialState);
  return (
    <IssueStateContext.Provider value={state}>
      <IssueDispatchContext.Provider value={dispatch}>
        {children}
      </IssueDispatchContext.Provider>
    </IssueStateContext.Provider>
  );
};
```
#### μ½λ©νΈ
  - λ¨λ°©ν₯ λ°μ΄ν° νλ¦μΌλ‘ λ³΅μ‘μ±μ μ€μΈμ μ΄ μΈμμ μ΄μμ΅λλ€. - μ‘°μ±νΈ

<br>

## 7. νλ‘μ νΈ μ€μΉ λ° μ€ν β¨

<br/>

1. Git Clone

```plaintext
$ git clone https://github.com/pre-onboading-2team/Week1_2_Issue_List.git
```

2. νλ‘μ νΈ ν¨ν€μ§ μ€μΉ

```plaintext
$ npm install
```

3. νλ‘μ νΈ μ€ν

```plaintext
$ npm start
```

