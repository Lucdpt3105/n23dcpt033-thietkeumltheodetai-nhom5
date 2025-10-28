%% Sơ đồ Hoạt động (Activity Diagram) cho quy trình học tập
activityDiagram
    title Quy trình Học tập của Sinh viên

    start
    :Đăng ký khóa học;
    
    partition "Vòng lặp học tập" {
        :Đọc tài liệu;
        if (Lựa chọn của sinh viên?) then (Làm Quiz)
            :Làm bài Quiz;
            :Xem lại kết quả;
            if (Đạt yêu cầu?) then (Có)
                :Hoàn thành bài học;
            else (Không)
                -> Đọc tài liệu;
            endif
        else (Thảo luận)
            :Thảo luận;
            -> Đọc tài liệu;
        endif
    }
    
    :Kết thúc bài học;
    stop

    %% Sơ đồ Trạng thái (State Diagram) cho một lượt làm bài thi
stateDiagram-v2
    title Trạng thái của một Lượt Làm Bài Thi

    [*] --> Chưa_bắt_đầu
    
    Chưa_bắt_đầu --> Đang_làm_bài: Bắt đầu làm bài
    Đang_làm_bài --> Đã_hoàn_thành: Nộp bài
    
    Đang_làm_bài --> Đã_hủy: Hủy bài / Hết giờ
    
    Đã_hoàn_thành --> [*]
    Đã_hủy --> [*]
