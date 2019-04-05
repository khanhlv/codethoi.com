+++
title = "Chủ đàn chó cắn bé trai tử vong: 'Tôi rất ân hận'"
description = "Sáng 5/4, bà Lê Thị An - chủ đàn chó cắn tử vong bé tr"
tags = ["test"]
keywords = ["enum","clean code"]
date = "2019-04-05"
+++
Sáng 5/4, bà Lê Thị An - chủ đàn chó cắn tử vong bé trai 7 tuổi ở thị trấn Lương Bằng, Kim Động (Hưng Yên) nói: "Hai ngày qua, tôi không thể nào ngủ được vì ân hận, thương cháu bé và không hiểu chuyện gì đang xảy ra".

Theo bà An, lúc cháu bé bị chó tấn công, bà đang đi điều tra dân số cùng một số cán bộ ở tổ dân phố, về đến nhà thấy sự việc nên vội lên xe cùng bố mẹ cháu đưa bé đến bệnh viện cấp cứu, nhưng đã quá muộn. Cháu bé bị đa chấn thương, mất nhiều máu và không qua khỏi.

"Tôi coi thằng bé như con cháu mình, vì từ khi cháu lọt lòng đến nay sống cùng bố mẹ trong khu nhà của tôi. Hàng ngày cháu thường chơi với đàn chó, thậm chí mấy chị em còn múc cháo cho chó ăn", bà An nói.

```Code
prepareSources.mustRunAfter operationProtocolFilter

task protocolZip(type: Zip, dependsOn: [operationProtocolFilter, protocolPdf]) {

    archiveName = "protocol-${projectConfig.versions.protocol}.zip"

    from(new File(project.buildDir, 'protocol')) {
        include '**'
        exclude protocolExcludes
        into project.name
    }

    from(project.buildDir) {
        include "Protocol.pdf"
    }

}
```
![TA](https://i-vnexpress.vnecdn.net/2019/04/05/56580495-305446870125760-89024-6469-9463-1554458329.jpg)