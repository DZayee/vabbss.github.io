---
bố cục: bài
title: Nhớ kinh nghiệm tổ chức CTF
thẻ: [CTF, ghi lại]
---

Có thể làm CTF mà không cần đánh tôi (: - P) <! - more ->

# Nguyên nhân
Một năm trước, tôi [đã trải nghiệm CTF] (/ 2019/12/16 / ctf.html), cảm giác rất thú vị và vì điều này, tôi thậm chí đã lên kế hoạch làm một [trò chơi] (/ 2019/12/17 / trò chơi. html). Thật tiếc là mọi người không thể làm được nữa, và họ không thể làm gì khác ngoài việc thủ thỉ.
Bất quá, mới vừa rồi không phải tham gia CTF, mà là trực tiếp đi cho người khác chơi CTF. Gần đây, hiệp hội của tôi phải ký hợp đồng với một cuộc thi CTF, với tư cách là bộ trưởng của hiệp hội, tôi đương nhiên phải tham gia vào cuộc thi đó. Điều tôi làm tốt nhất là vận hành và bảo trì, vì vậy trong cuộc thi này, tôi trở thành người chịu trách nhiệm duy trì hoạt động và bảo trì nền tảng CTF.

# Cảm xúc
Sau khi trở thành người duy trì hệ thống CTF, tôi hiểu sâu hơn về CTF. Bản chất của hệ thống CTF là một bảng điểm cộng với một máy đích và sau đó chỉ là một số câu hỏi. Các câu hỏi như Web và PWN yêu cầu một máy đích . Khác Đối với Crypto, Reverse, Misc, v.v., bạn chỉ cần đặt tiêu đề vào máy chủ tệp. Ngoài ra, cách tính điểm cũng rất đơn giản, bạn chỉ cần phán đoán kết quả có bằng cờ đặt là xong rồi cho điểm theo đáp án.
Nói chung, cờ trong các sự kiện chính thức có vẻ là động và cờ của mỗi đội là khác nhau, và sau đó tất cả các máy bay không người lái do mỗi đội bắn đều được cách ly với docker. CTF do chúng tôi tổ chức không chuyên nghiệp. Nó chỉ có thể được coi là một tương đối nghiệp dư.

# kinh nghiệm
Trong CTF này, tôi không muốn quan tâm đến nền tảng. Nếu tôi định xây dựng nền tảng này, tôi có thể chọn [CTFd] (https://github.com/CTFd/CTFd) làm nền tảng của CTF này. Tuy nhiên, CTF này đã được tổ chức vài lần trước khi tôi đến và họ đã sử dụng [FBCTF] (https://github.com/facebookarchive/fbctf) do Facebook phát triển làm nền tảng cho toàn bộ cuộc thi. Vì là vận hành và bảo trì nên chắc chắn tôi không quan tâm đến thủ tục nên cứ để họ làm những việc liên quan.
Tuy nhiên, thực tế đã chứng minh đây là một quyết định sai lầm, nền tảng này không còn được bảo trì, tuy nhìn rất ưa nhìn nhưng lại có rất nhiều lỗi, điều này đã mang lại rất nhiều áp lực cho đội ngũ bảo trì của chúng tôi trong trò chơi này. Ví dụ: [câu này] (https://github.com/facebookarchive/fbctf/blob/4ec9b6be404fce1bed6d1066fccf10c4255767bb/database/countries.sql#L161) trong nền tảng này đã mang lại cho chúng tôi rất nhiều rắc rối. Chỉ trong một câu nói ngắn gọn như vậy, nền tảng đang chạy đã trực tiếp buộc phải ngừng chạy. tại sao? Rất đơn giản, bởi vì trường học của tôi là Trung Quốc, những chuyện như thế này không được phép xảy ra ...
Ngoài ra, FBCTF này cũng rất hấp dẫn, mã chỉ là PHP thông thường, nhưng phần mềm và phương pháp sử dụng để triển khai là khác nhau. Thông thường, loại này có thể giải quyết vấn đề với LEMP hoặc LAMP, và nó phải có môi trường hhvm, nhưng môi trường không phải của tôi, và tôi không quan tâm nó được sử dụng để làm gì. Tuy nhiên, có vấn đề với i18n của nó. Trong [dòng này] (https://github.com/facebookarchive/fbctf/blob/4ec9b6be404fce1bed6d1066fccf10c4255767bb/src/controllers/IndexController.php#L598), hàm của `tr` không thêm, và sau đó đăng ký Khi nó được hiển thị, sẽ có một vấn đề. Không quan trọng là có vấn đề gì, đại sự là muốn thay đổi, nhưng không có phản ứng gì sau cái này hỏng bét đổi? Mình làm lâu rồi mà chưa làm tốt, sau này mới biết do nó sử dụng hhvm nên cái này sẽ biên dịch mã php rồi sửa đổi trực tiếp mã nhưng không có gì xảy ra cả. Bạn phải sử dụng `hhvm-repo-mode` để cập nhật mã 😓 ......
Cái khác là cơ sở dữ liệu. Người triển khai đã không thay đổi bộ ký tự vào thời điểm đó. Thay vào đó, bộ ký tự Latinh đã được sử dụng. Khi lưu trữ các ký tự Trung Quốc, sẽ có tất cả các loại mã bị cắt xén. Dù sao thì tôi cũng không thể lấy lại được , nhưng chương trình dường như không bị ảnh hưởng. Vì vậy, hãy quên nó đi.
Người lãnh đạo cũng có những nhu cầu mới. Đây coi như là một kinh nghiệm đi trước trong cuộc đời công ty. Lãnh đạo nói rằng sẽ bổ sung thêm một tính năng. Tôi chắc chắn sẽ không nghĩ đến việc nhặt được lỗ hổng lớn này. nhiệm vụ này được giao cho giáo viên PHP của chúng tôi, nhưng giáo viên này thực sự rất chuyên nghiệp. Cuối cùng thì cũng phải mất 4 giờ để hoàn thành công việc và trình độ đã được xác định.
Cuộc cạnh tranh hiện tại vẫn chưa kết thúc, tôi không biết điều gì mới và không thể giải thích được sẽ xảy ra, vì vậy hãy theo dõi ~
