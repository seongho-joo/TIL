# readXLSX

- npm을 사용해서 xlsx 모듈 설치  
   \$ npm i xlsx

## code

        const fs = require('fs')
        const XLSX = require('xlsx')

        let buf = fs.readFileSync('test.xls')
        let wb = XLSX.read(buf, { type: 'buffer' })

        wb.SheetNames.forEach((sheetName) => {
            console.log('sheetName: ' + sheetName)

            let rows = XLSX.utils.sheet_to_json(wb.Sheets[sheetName])
            console.log(rows)
        })

## Result

| <img src='/Users/seongho/Desktop/ScreenShot/a.png' /> | <img src='/Users/seongho/Desktop/ScreenShot/res.png' /> |
| ----------------------------------------------------- | ------------------------------------------------------- |

