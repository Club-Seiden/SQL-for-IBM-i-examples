-- This should work for 7.1 and above. Just some simple math to get a bead on user security statistics. 
-- The only DB2 for i Service it hits is QSYS2.USER_INFO.

BEGIN
-- Count total users
DECLARE all_users DEC(7, 0);
-- Users with Special Authorities
DECLARE users_with_spcaut DEC(7, 0);
DECLARE pct_users_with_spcaut DEC(5, 2);
DECLARE users_with_splctl DEC(7, 0);
DECLARE pct_users_with_splctl DEC(5, 2);
DECLARE users_with_allobj DEC(7, 0);
DECLARE pct_users_with_allobj DEC(5, 2);
DECLARE users_with_jobctl DEC(7, 0);
DECLARE pct_users_with_jobctl DEC(5, 2);
DECLARE users_with_secadm DEC(7, 0);
DECLARE pct_users_with_secadm DEC(5, 2);
DECLARE users_with_audit DEC(7, 0);
DECLARE pct_users_with_audit DEC(5, 2);
DECLARE users_with_savsys DEC(7, 0);
DECLARE pct_users_with_savsys DEC(5, 2);
DECLARE users_with_iosyscfg DEC(7, 0);
DECLARE pct_users_with_iosyscfg DEC(5, 2);
DECLARE users_with_service DEC(7, 0);
DECLARE pct_users_with_service DEC(5, 2);
DECLARE users_with_pwdnone DEC(7, 0);
DECLARE pct_users_with_pwdnone DEC(5, 2);
DECLARE users_signon_90days DEC(7, 0);
DECLARE pct_users_signon_90days DEC(5, 2);
DECLARE users_signon_never DEC(7, 0);
DECLARE pct_users_signon_never DEC(5, 2);
DECLARE users_pwd_expired DEC(7, 0);
DECLARE pct_users_pwd_expired DEC(5, 2);
DECLARE users_pwd_none DEC(7, 0);
DECLARE pct_users_pwd_none DEC(5, 2);
DECLARE users_lmtcpl DEC(7, 0);
DECLARE pct_users_lmtcpl DEC(5, 2);
DECLARE users_disabled DEC(7, 0);
DECLARE pct_users_disabled DEC(5, 2);
DECLARE group_profiles_pwd DEC(7, 0);
DECLARE pct_group_profiles_pwd DEC(5, 2);
DECLARE users_pwd_expint DEC(7, 0);
DECLARE pct_users_pwd_expint DEC(5, 2);
SET all_users = (SELECT COUNT(AUTHORIZATION_NAME)
                 FROM QSYS2.USER_INFO);
SET users_with_spcaut = (SELECT COUNT(AUTHORIZATION_NAME)
                         FROM QSYS2.USER_INFO
                         WHERE SPECIAL_AUTHORITIES <> '');
SET pct_users_with_spcaut = (users_with_spcaut / all_users) * 100;
SET users_with_splctl = (SELECT COUNT(AUTHORIZATION_NAME)
                         FROM QSYS2.USER_INFO
                         WHERE SPECIAL_AUTHORITIES LIKE '%*SPLCTL%');
SET pct_users_with_splctl = (users_with_splctl / all_users) * 100;
SET users_with_allobj = (SELECT COUNT(AUTHORIZATION_NAME)
                         FROM QSYS2.USER_INFO
                         WHERE SPECIAL_AUTHORITIES LIKE '%*ALLOBJ%');
SET pct_users_with_allobj = (users_with_allobj / all_users) * 100;
SET users_with_jobctl = (SELECT COUNT(AUTHORIZATION_NAME)
                         FROM QSYS2.USER_INFO
                         WHERE SPECIAL_AUTHORITIES LIKE '%*JOBCTL%');
SET pct_users_with_jobctl = (users_with_jobctl / all_users) * 100;
SET users_with_secadm = (SELECT COUNT(AUTHORIZATION_NAME)
                         FROM QSYS2.USER_INFO
                         WHERE SPECIAL_AUTHORITIES LIKE '%*SECADM%');
SET pct_users_with_secadm = (users_with_secadm / all_users) * 100;
SET users_with_iosyscfg = (SELECT COUNT(AUTHORIZATION_NAME)
                           FROM QSYS2.USER_INFO
                           WHERE SPECIAL_AUTHORITIES LIKE '%*IOSYSCFG%');
SET pct_users_with_iosyscfg = (users_with_iosyscfg / all_users) * 100;
SET users_with_service = (SELECT COUNT(AUTHORIZATION_NAME)
                          FROM QSYS2.USER_INFO
                          WHERE SPECIAL_AUTHORITIES LIKE '%*SERVICE%');
SET pct_users_with_service = (users_with_service / all_users) * 100;
-- users with Password as 



SET users_with_pwdnone = (SELECT COUNT(AUTHORIZATION_NAME)
                          FROM QSYS2.USER_INFO
                          WHERE NO_PASSWORD_INDICATOR = 'YES');
SET pct_users_with_pwdnone = (users_with_pwdnone / all_users) * 100;
-- Users who havent signed on in 90 days
SET users_signon_90days = (SELECT COUNT(AUTHORIZATION_NAME)
                           FROM QSYS2.USER_INFO
                           WHERE ADD_MONTHS(CURRENT_TIMESTAMP, -3) >
                           PREVIOUS_SIGNON);
SET pct_users_signon_90days = (users_signon_90days / all_users) * 100;
-- Users who have never signed on
SET users_signon_never = (SELECT COUNT(AUTHORIZATION_NAME)
                          FROM QSYS2.USER_INFO
                          WHERE PREVIOUS_SIGNON IS NULL);
SET pct_users_signon_never = (users_signon_never / all_users) * 100;
    -- Users with password set to expired
SET users_pwd_expired = (SELECT COUNT(AUTHORIZATION_NAME)
                              FROM QSYS2.USER_INFO
                              WHERE SET_PASSWORD_TO_EXPIRE = 'YES');
SET pct_users_pwd_expired = (users_pwd_expired / all_users) * 100;
    -- Users with password of *NONE
SET users_pwd_none = (SELECT COUNT(AUTHORIZATION_NAME)
                           FROM QSYS2.USER_INFO
                           WHERE NO_PASSWORD_INDICATOR = 'YES');
SET pct_users_pwd_none = (users_pwd_none / all_users) * 100;
SET users_lmtcpl = (SELECT COUNT(AUTHORIZATION_NAME)
                                FROM QSYS2.USER_INFO
                                WHERE LIMIT_CAPABILITIES = '*YES');
SET pct_users_lmtcpl = (users_lmtcpl / all_users) * 100;
SET users_disabled = (SELECT COUNT(AUTHORIZATION_NAME)
                      FROM QSYS2.USER_INFO
                      WHERE STATUS = '*DISABLED');
SET pct_users_disabled = (users_disabled / all_users) * 100;
SET group_profiles_pwd = (SELECT COUNT(AUTHORIZATION_NAME)
                          FROM QSYS2.USER_INFO
                          WHERE GROUP_ID_NUMBER <> 0 AND
                          NO_PASSWORD_INDICATOR = 'NO');
SET pct_group_profiles_pwd = (group_profiles_pwd / all_users) * 100;
SET users_pwd_expint = (SELECT COUNT(AUTHORIZATION_NAME)
                        FROM QSYS2.USER_INFO
                        WHERE PASSWORD_EXPIRATION_INTERVAL <> 0);
SET pct_users_pwd_expint = (users_pwd_expint / all_users) * 100;
--create the userstats table



CREATE TABLE qtemp.userstats(description CHAR(75),amount INT,percent
DEC(5, 2));
-- insert scripts
INSERT INTO qtemp.userstats(description,amount)
VALUES ('Total Users',all_users);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES
('Users with Special Authorities',users_with_spcaut,pct_users_with_spcaut);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES ('Users with *SPLCTL',users_with_splctl,pct_users_with_splctl);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES ('Users with *ALLOBJ',users_with_allobj,pct_users_with_allobj);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES ('Users with *JOBCTL',users_with_jobctl,pct_users_with_jobctl);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES ('Users with *SECADM',users_with_secadm,pct_users_with_secadm);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES ('Users with *IOSYSCFG',users_with_iosyscfg,pct_users_with_iosyscfg);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES ('Users with *SERVICE',users_with_service,pct_users_with_service);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES
('Users not signed-on in 90 days',users_signon_90days,pct_users_signon_90days);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES
('Users who have never signed on',users_signon_never,pct_users_signon_never);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES
('Users with password expired',users_pwd_expired,pct_users_pwd_expired);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES
('Users with password set to *NONE',users_pwd_none,pct_users_pwd_none);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES
('Users with limited capabilities set to *YES',users_lmtcpl,pct_users_lmtcpl);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES ('Disabled User Profiles',users_disabled,pct_users_disabled);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES
('Group profiles with passwords',group_profiles_pwd,pct_group_profiles_pwd);
INSERT INTO qtemp.userstats(description,amount,percent)
VALUES
('Users with password sysval override',users_pwd_expint,pct_users_pwd_expint);
END;
select * from qtemp.userstats;
