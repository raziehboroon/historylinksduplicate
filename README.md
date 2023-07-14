# historylinksduplicate

import "./Navbar.scss";
import React, { useEffect, useRef, useState } from "react";
import { Link } from "react-router-dom";
// Component(s)
import Sidebar from "../Sidebar/Sidebar";
// Translator
import { useTranslation } from "react-i18next";

const Navbar = () => {
  const { t } = useTranslation();
  const historyContainerRef = useRef();
  const [showSidebar, setShowSidebar] = useState(false);
  const [showHistory, setShowHistory] = useState(false);
  const [showMore, setShowMore] = useState({ isVisible: true });

  const links = [
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
    { title: "home", href: "www.home.com", time: "" },
  ];

  useEffect(() => {
    const handleClickOutsideHistoryContainer = (event) => {
      //ref is undefined???
      console.log("clicked: ", historyContainerRef);
      if (
        historyContainerRef.current &&
        !historyContainerRef.current.contains(event.target)
      ) {
        console.log("false");
        setShowHistory(false);
      } else {
        console.log("true");
        setShowHistory(true);
      }
    };

    document.addEventListener("mousedown", handleClickOutsideHistoryContainer);
  });

  console.log("current tab: ", window.location);

  return (
    <nav>
      <div className="navbar">
        <div className="history-btn" onClick={() => setShowHistory(true)}>
          History
          {showHistory && (
            <div
              className={`history-links-container ${
                !showMore.isVisible && "expanded-history-links-container"
              }`}
            >
              <div className="history-content">
                <div
                  className={`links-container ${
                    !showMore.isVisible && "expanded-links-container"
                  }`}
                >
                  {links?.map((item, index) => (
                    <Link
                      className="link"
                      to={item.href}
                      key={index}
                      onClick={() => setShowHistory(false)}
                    >
                      {item.title}
                    </Link>
                  ))}
                </div>
                {showMore.isVisible && (
                  <div
                    className="show-more-btn"
                    onClick={() => setShowMore({ isVisible: false })}
                  >
                    show more
                  </div>
                )}
              </div>
            </div>
          )}
        </div>
        {!showSidebar && (
          <button className="nav-btn" onClick={() => setShowSidebar(true)}>
            {t("nav_btn")}
          </button>
        )}
      </div>
      <Sidebar showSidebar={showSidebar} setShowSidebar={setShowSidebar} />
    </nav>
  );
};

export default Navbar;



@import "../../App.scss";

nav {
  max-width: 100vw;
  height: 5rem;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  transition: $transition;
  z-index: 10;
}

.navbar {
  height: 100%;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: wheat;
  padding: 0 2rem;
  background-color: transparent;
  direction: ltr;
  .nav-logo {
    height: 3.5rem;
    // left: 1rem;
  }

  .history-btn {
    position: relative;
    margin-left: 2rem;
    padding: 0.2rem 0.4rem;
    background-color: blueviolet;
    color: white;

    .history-links-container {
      position: absolute;
      top: 5px;
      left: 5px;
      background-color: pink;
      border-radius: 0.3rem;
      color: white;
      width: 10rem;
      height: 30vh;

      .history-content {
        height: 100%;
        width: 100%;
        position: relative;
        .links-container {
          height: 70%;
          overflow-y: hidden;
          .link {
            text-decoration: none;
            display: block;
            color: darkblue;
            padding: 0 0.5rem;
            text-transform: capitalize;
          }
        }
        .expanded-links-container {
          height: 100%;
          overflow-y: scroll;
        }
        .show-more-btn {
          position: absolute;
          text-transform: capitalize;
          left: 0;
          bottom: 0;
          right: 0;
          text-align: center;
          color: darkgray;
          border-top: 0.2rem solid darkgray;
          &:hover {
            cursor: pointer;
          }
        }
      }
    }
    .expanded-history-links-container {
      height: 80vh;
      transition: all 0.3s ease-in-out;
    }
  }

  .nav-btn {
    padding: 0.5rem 1rem;
    border: none;
    text-transform: uppercase;
    font-weight: bold;
    border-radius: 0.02rem;
    background-color: $clr-white;
    color: $clr-black;
    transition: $transition;
    box-shadow: $light-shadow;
    // right: 1rem;

    &:hover {
      color: $clr-white;
      background-color: $clr-hover;
    }
  }
}
