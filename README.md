# local_timestamps
operations on a local timestamp (UNIX) 



    #[allow(deprecated)]
    #[test]
    fn t001_lts1() {
        let date_str = "2000-01-01";
        let ts = lts_date_string_to_timestamp(date_str);
        let date_time_str =  lts_to_date_time_string(ts.unwrap());
        assert_eq!(date_time_str,"2000-01-01 00:00:00");

        let now = Utc::now().timestamp();
        let offset = Local.timestamp(now, 0).offset().fix().local_minus_utc() as i64; 
        let utc_adjusted = now + offset;
        let utc_adjusted_str = lts_to_date_time_string(utc_adjusted);
        let new_now = lts_now();
        let new_now_str = lts_to_date_time_string(new_now);
        assert_eq!(new_now_str,utc_adjusted_str);

        let date_str2 = "2000-01-01";
        let ts2 = lts_date_string_to_timestamp(date_str2);
        let date_time_str2 =  lts_to_date_string(ts2.unwrap());
        assert_eq!(date_time_str2,"2000-01-01");
        assert_eq!(1,1);
    }




    #[allow(deprecated)]
    #[test]
    fn t002_recur_term() {
        let date_str = "2000-01-01";
        let term = "+3m";
        let ts = lts_date_string_to_timestamp(date_str);
        let res = lts_add_timestamp_to_recur_term(ts.unwrap(),term);
        let res_time = lts_to_date_time_string(res.unwrap());
        assert_eq!(res_time,"2000-04-01 00:00:00".to_string());

        let date_str2 = "2000-01-01";
        let term2 = "+17d";
        let ts2 = lts_date_string_to_timestamp(date_str2);
        let res2 = lts_add_timestamp_to_recur_term(ts2.unwrap(),term2);
        let res_time2 = lts_to_date_time_string(res2.unwrap());
        assert_eq!(res_time2,"2000-01-18 00:00:00".to_string());

        let date_str3 = "2000-01-01";
        let term3 = "+6w";
        let ts3 = lts_date_string_to_timestamp(date_str3);
        let res3 = lts_add_timestamp_to_recur_term(ts3.unwrap(),term3);
        let res_time3 = lts_to_date_time_string(res3.unwrap());
        assert_eq!(res_time3,"2000-02-12 00:00:00".to_string());

        let date_str = "2000-01-27";
        let term = "+17y";
        let ts = lts_date_string_to_timestamp(date_str);
        let res = lts_add_timestamp_to_recur_term(ts.unwrap(),term);
        let res_time = lts_to_date_time_string(res.unwrap());
        assert_eq!(res_time,"2017-01-27 00:00:00".to_string());
        
        // something with now
        let now_utc = Utc::now().timestamp();
        let offset = Local.timestamp(now_utc, 0).offset().fix().local_minus_utc() as i64;
        let add = now_utc + offset;
        assert_eq!(add,lts_now());
    }




