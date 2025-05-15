- 미션 기록
    1. 응답 통일화
        1. index.js
            
            ```jsx
            app.use((req, res, next)=> {
              res.success = (result) => {
                return res.json({
                  resultType: "success",
                  error: null,
                  result: result
                })
              }
            
              res.error = ({
                errorCode = "unknown",
                statusCode,
                reason = null,
                data = null
              }) => {
                return res.json({
                  resultType: "error",
                  error: {
                    errorCode, reason, data
                  },
                  result: null
                })
              }
            
              next();
            });
            ```
            
            app.use 내에서 success, error라는 res 함수를 선언하고 있다. 각각 성공, 실패했을 때 처리를 하고 결과를 json형식으로 반환하고 있다.
            
        2. error.js
            
            ```jsx
            import { StatusCodes } from "http-status-codes";
            export class DuplicateDataError extends Error{
                errorCode = 'E001';
                statusCode = StatusCode.BAD_REQUEST;
                constructor(reason, data){
                    super(reason);
                    this.reason = reason || '이미 존재하는 데이터입니다.';
                    this.data = data;
                }
            }
            
            export class NoDataFoundError extends Error{
                errorCode = 'E002';
                statusCode = StatusCodes.NOT_FOUND
                constructor(reason, data){
                    super(reason);
                    this.reason = reason || '데이터를 찾을 수 없습니다.';
                    this.data = data;
                }
            }
            ```
            
            에러 객체 하나하나를 구현한 것. 생성자에서 이유와 data를 받아서 이유와 어떤 값이 잘못되었는지 출력할 수 있게 하였다.