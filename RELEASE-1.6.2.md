# PubStar Mobile Ads SDK — Release 1.6.2

**Ngày phát hành:** 2026-09-24
**Phạm vi:** iOS · Android · React Native · Flutter · Unity

---

## 🔭 Tổng quan
Phiên bản 1.6.2 tập trung vào **báo cáo (report)** và **sửa lỗi tích hợp**: bổ sung chỉ số crash/session và thời gian tải, gắn thông tin màn hình (screen) cho mọi chỉ số, thống nhất cách đo thời gian hiển thị giữa iOS và Android, và sửa các lỗi khiến SDK không khởi tạo được trên React Native / Unity. Bản này cũng đưa các plugin React Native, Flutter, Unity lên đúng SDK gốc 1.6.2 — trước đây các plugin vẫn trỏ về SDK gốc 1.6.0.

## ✨ Tính năng chung (mọi nền tảng)
- **Crash & session:** SDK tự ghi nhận `app_crash` và `app_session` để tính **Crash Rate** trên Statistics Report. Crash được lưu lại lúc xảy ra và gửi ở lần mở app kế tiếp.
- **Màn hình (screen):** mọi chỉ số báo cáo đều mang thông tin màn hình nơi quảng cáo được yêu cầu, không chỉ các chỉ số lúc hiển thị.
- **Thời gian tải (`load_time`):** đo thời gian từ lúc yêu cầu tới lúc quảng cáo tải xong.
- **Thời gian hiển thị (`display_time`):** banner/native đo thời gian quảng cáo nằm trên màn hình; quảng cáo toàn màn hình (interstitial, rewarded, app open) đo **time-to-show** — khoảng chờ từ lúc tải xong tới lúc người dùng thấy quảng cáo. iOS và Android giờ đo giống nhau.
- **Impression:** tối đa một lượt `impression` cho mỗi `sdk_request` trên một vị trí quảng cáo, tránh đếm trùng.
- **Phiên bản SDK trong báo cáo:** mỗi báo cáo mang nền tảng tích hợp và phiên bản, ví dụ `ios-1.6.2`, `android-1.6.2`, `unity-1.6.2`.

## ⚠️ Thay đổi hành vi
- **iOS bắt buộc khai `io.pubstar.key`.** Thiếu hoặc để trống key trong `Info.plist`, SDK dừng ngay lúc khởi tạo — giống Android từ trước tới nay. Các bản cũ âm thầm dùng App ID debug dựng sẵn: app vẫn chạy bình thường nhưng mọi báo cáo, kể cả session và crash, đổ về app debug. App nào đang thiếu key sẽ **crash lúc khởi động** sau khi nâng lên 1.6.2 — xem [Troubleshooting](ios/troubleshooting.md).

## 📱 Chi tiết theo nền tảng

| Nền tảng | Phiên bản | Điểm chính của 1.6.2 |
|----------|-----------|----------------------|
| **iOS** | `1.6.2` | Bắt buộc `io.pubstar.key`; `display_time` time-to-show cho quảng cáo toàn màn hình; sửa `display_time` của banner/native bị ngắt sớm khi adapter dọn view chứa; sửa `sdkVersion` báo `unknown` khi link tĩnh; chặn crash khi `sdkKey` AppLovin sai định dạng (gộp hotfix 1.6.0-1). |
| **Android** | `1.6.2` | `app_session` gửi đúng `appVersion` (trước đây để trống); adapter mediation **AdMob** và **AppLovin MAX** lần đầu có trên Maven Central (`io.pubstar.mediation.adapter.admob`, `io.pubstar.mediation.adapter.applovin`). |
| **React Native** | `1.6.2` | Dùng SDK gốc 1.6.2 (Android trước đây ghim cứng `1.6.0`); sửa lỗi iOS khởi tạo thất bại với mã `-7` ở bản Release khi gọi `initialization()` ngay lúc mở app. |
| **Flutter** | `1.6.2` | Dùng SDK gốc 1.6.2 (Android trước đây ghim cứng `1.6.0`). |
| **Unity** | `1.6.2` | `.unitypackage` đã có đủ bridge native Android và iOS (thiếu từ 1.5.0 đến 1.6.1); sửa lỗi iOS khởi tạo thất bại với mã `-7`; build iOS không còn ghi đè `io.pubstar.key` và `GADApplicationIdentifier` mà publisher đã khai. |

## 🔌 Mạng quảng cáo hỗ trợ (1.6.2)
Không đổi so với 1.6.0.
- **iOS:** Google AdMob, AppLovin MAX, Google IMA, Pangle, Unity Ads, Vungle, Mintegral, InMobi.
- **Android:** Google AdMob, AppLovin MAX, Meta Audience Network, Pangle, Unity Ads, Vungle, Mintegral, InMobi, Yandex, Appodeal, Google IMA.

## 📦 Định dạng quảng cáo hỗ trợ
Banner · Native · Native tùy biến · Interstitial · App Open · Rewarded · Video (IMA)

## ⚠️ Lưu ý phát hành
- **iOS:** kiểm tra `Info.plist` đã có `io.pubstar.key` là App ID thật của app trước khi phát hành bản dùng 1.6.2.
- **Unity:** import bản 1.6.2 đè lên bản đang dùng là đủ. Nếu project từng cài **1.3.1**, xoá thêm thư mục `Assets/Plugins/Android/PubStar.androidlib/build/` — xem [Upgrading to 1.6.2](unity/integration.md). Publisher nâng cấp từ các bản 1.5.0–1.6.1 sẽ lần đầu nhận bridge native mới, nên SDK Android có thể nhảy thẳng từ bản cũ lên 1.6.2.
- **Android mediation:** tài liệu 1.6.0 hướng dẫn cài `io.pubstar.mediation.adapter.admob:ads:1.6.0` / `...applovin:ads:1.6.0`, nhưng các bản này chưa từng có trên Maven Central. Hãy dùng `1.6.2`.
- **iOS:** sau khi cập nhật SDK hoặc adapter cần chạy lại `pod install`.

---

*Tài liệu hướng dẫn chi tiết: https://pub-star.gitbook.io/docs/*
