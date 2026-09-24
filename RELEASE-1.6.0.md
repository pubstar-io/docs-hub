# PubStar Mobile Ads SDK — Release 1.6.0

**Ngày phát hành:** 2026-06-18
**Phạm vi:** iOS · Android · React Native · Flutter

---

## 🔭 Tổng quan
Phiên bản 1.6.0 đồng bộ tính năng trên tất cả nền tảng, tập trung vào: **Native tùy biến giao diện**, **quảng cáo Video theo chuẩn Google IMA**, khả năng **chạy PubStar bên trong Google AdMob / AppLovin MAX**, và **báo cáo doanh thu lên Firebase/GA4 phục vụ ROAS**.

## ✨ Tính năng chung (mọi nền tảng)
- **Native tùy biến giao diện:** cho phép tự thiết kế layout cho quảng cáo native (tiêu đề, mô tả, icon, media, nút CTA…) khớp với giao diện app.
- **Video (IMA):** tích hợp Google IMA, hỗ trợ cả **in-stream** và **out-stream**.
- **PubStar Mediation:** PubStar tham gia đấu giá như một network bên trong **Google AdMob** và **AppLovin MAX**.
- **Báo cáo doanh thu cho ROAS:** tự gửi doanh thu ước tính theo từng lượt hiển thị và sự kiện click lên Firebase/Google Analytics, phục vụ theo dõi và tối ưu chiến dịch theo ROAS.
- **GDPR / UMP consent:** xin đồng thuận người dùng trước khi khởi tạo SDK.
- **OpenRTB (ORTB) bidding:** cập nhật và sửa báo cáo ORTB.
- **Tài liệu & README** được làm mới, đồng bộ giữa các nền tảng.

## 📱 Chi tiết theo nền tảng

| Nền tảng | Phiên bản | Điểm chính của 1.6.0 |
|----------|-----------|----------------------|
| **iOS** | `1.6.0` | Video IMA (out-stream); chạy mediation trong AdMob/MAX; xin đồng thuận GDPR/UMP khi khởi tạo; báo cáo doanh thu lên Firebase cho ROAS; tài liệu đầy đủ. |
| **Android** | `1.6.0` | Gộp Video IMA vào mediation AdMob/MAX; triển khai PubStar Mediation cho AdMob & MAX (banner, native, interstitial, app open, rewarded); Native tùy biến giao diện; báo cáo doanh thu lên Firebase cho ROAS. |
| **React Native** | `1.6.0` | Native tùy biến giao diện; Video IMA (in-stream/out-stream); sửa lỗi banner/native không hiển thị trên Android dù tải & hiển thị thành công; kế thừa báo cáo ROAS từ nền tảng gốc. |
| **Flutter** | `1.6.0` | Native tùy biến giao diện; Video IMA (in-stream/out-stream); tài liệu đầy đủ; kế thừa báo cáo ROAS từ nền tảng gốc. |

## 🔌 Mạng quảng cáo hỗ trợ (1.6.0)
- **iOS:** Google AdMob, AppLovin MAX, Google IMA, Pangle, Unity Ads, Vungle, Mintegral, InMobi.
- **Android:** Google AdMob, AppLovin MAX, Meta Audience Network, Pangle, Unity Ads, Vungle, Mintegral, InMobi, **Yandex**, **Appodeal**, Google IMA.

## 📦 Định dạng quảng cáo hỗ trợ
Banner · Native · Native tùy biến · Interstitial · App Open · Rewarded · **Video (IMA)**

## ⚠️ Lưu ý phát hành
- Báo cáo ROAS yêu cầu app **có tích hợp Firebase/Google Analytics**; tránh đếm trùng lượt hiển thị với AdMob.
- **React Native:** bản trên npm hiện là `1.6.0-1` và đang là phiên bản mới nhất; nếu muốn người dùng cài theo dải `^1.6.0` cũng nhận được, nên nâng lên `1.6.1`.
- **iOS:** sau khi cập nhật adapter cần cài lại CocoaPods.

---

*Tài liệu hướng dẫn chi tiết: https://pub-star.gitbook.io/docs/*
